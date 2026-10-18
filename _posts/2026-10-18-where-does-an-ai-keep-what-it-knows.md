---
title: "Where Does an AI Keep What It Knows?"
description: "Weights, documents, knowledge bases and search, and how an agent chooses between them."
tags: [agents, retrieval, rag, knowledge-graphs, search]
toc: true
---

A delivery form asks for your phone number. You know it by heart, so you just type it in. What about your partner's number? It's probably two taps away on your phone. A plumber's number? That's something you search for if and when the dishwasher breaks. Nobody taught you this system, but you use it all the time: the number you need most lives in your head, the ones you need now and then are saved somewhere easy to reach, and the ones you rarely need you look up. AI agents face the same choice, many times in a single task. Where they keep what they know, and how they decide where to look, is a large part of what makes them useful or unreliable.

The [last post]({% post_url 2026-10-04-why-we-dream-and-why-ai-is-starting-to %}) was about how memory works: fast and slow systems, sleep and forgetting. This one is about those three places, the head, the notes and the search, and how an agent decides which one to reach for when it needs to know something.

## Three places to keep what you know

People have always split knowledge three ways. Some of it is in our heads. Some of it is in our notes: diaries, files, a notebook. The rest is out in the world, in libraries, on the internet and in other people's heads, waiting to be looked up.

In the [first post]({% post_url 2026-09-28-what-does-a-machine-actually-know %}) we met Otto, the man in Andy Clark and David Chalmers's thought experiment who relies on a notebook in place of his memory. Their argument was that if a notebook does the job of memory, it counts as part of the mind (Clark & Chalmers, 1998). AI agents are built along the same lines. Their knowledge doesn't sit in one place but is spread across three.

|  | For a person | For an agent | Good at | Bad at |
| --- | --- | --- | --- | --- |
| **Know it** | What's in your head | The model's weights | Speed, fluency, language and general skills | Going stale, citing sources, being corrected |
| **Note it** | Your notes and files | Files, search indexes, vector stores, databases, knowledge graphs | Trusted, private and curated facts | The cost of building and maintaining them |
| **Look it up** | The library, an expert | Web search, APIs, connectors | Freshness and breadth | Speed, cost and uneven sources |

## Know it: the weights

Everything a model learned in training lives in its weights, billions of numbers that encode language, facts and skills, including the learned procedures it uses to work through problems. Michael Polanyi argued that "we can know more than we can tell". We can recognise a familiar face among thousands, yet can't say exactly how we do it (Polanyi, 1966). A model's weights hold something like tacit knowledge. Though they were learned from explicit text, what the model ends up with is not a copy of that text. It is a web of patterns that it uses fluently but cannot lay out. In 2025, Anthropic's researchers traced how one of their Claude models adds two numbers and found it working along parallel internal paths. Yet when asked how it did the sum, it described the carry-the-one method taught at school (Lindsey et al., 2025). A plausible story, but not what actually happened. Ask a model where it learned something and you get the same kind of reconstruction.

This is semantic memory (see the [previous post]({% post_url 2026-10-04-why-we-dream-and-why-ai-is-starting-to %})), which captures mostly the gist without the source. Much like the brain's slow learning system, which learns from what many experiences have in common, model training abstracts from many millions of input documents. That's why a model can generalise and answer questions it wasn't explicitly trained on. The price is that many of the specifics are gone, and with them any built-in record of where the knowledge came from.

However powerful this is, it has some inherent limitations. First, and most visible in early chatbots that couldn't search, the knowledge goes stale, because there's a cutoff date tied to when training stopped. Second, because the sources aren't stored in the traditional sense, the model can't cite them directly; it can only reproduce what it learned from them. This leads to the third limitation. The stored knowledge is hard to correct because it's hard to trace. Researchers have shown that individual facts can be located and edited inside a model's weights (Meng et al., 2022). But this work is fragile, and it isn't how production models are kept up to date when a fact changes.

So the weights are best used for what they're good at: language, general skills such as summarising or working through a problem, and broad background knowledge. Anything that changes, needs a source or belongs to you has to live somewhere else.

## Note it: documents and knowledge bases

The second place is the agent's own notes. That is knowledge you or the agent chose, stored outside the model, for example as a .md file, a database, or a graph.

**Plain files.** The simplest store is a text file the agent reads every time it starts, such as a README, a set of instructions or a CLAUDE.md file describing a project's conventions. It works when the notes are small enough to fit within a model's context window, which is often enough in practice, and it needs no infrastructure.

**Index & keyword search.** Often overlooked because it's been around for decades, a search index such as Elasticsearch or OpenSearch ranks documents with methods like BM25 (Robertson & Zaragoza, 2009). It matches words rather than meanings, which makes it especially useful for exact names, IDs and codes. It remains a core part of many RAG systems, often alongside vector search.

**Vector stores.** Retrieval-augmented generation (Lewis et al., 2020) popularised turning each chunk of text into an embedding, storing all embeddings in advance, and retrieving the chunks whose meaning is closest to the question at query time. Though this finds paraphrases that keyword search misses, it often fails on exact terms. Many production systems now run a hybrid of the two approaches.

**Databases behind tools.** Plenty of knowledge is structured or semi-structured and lives in SQL databases or behind an internal API. An agent can be given tools to access it directly rather than copying everything into a document store.

**Knowledge graphs.** Last are knowledge graphs, i.e. entities connected by typed relationships. The idea goes back to the 1960s, when Ross Quillian proposed that human semantic memory is organised as a network of linked concepts (Quillian, 1968). Fast forward to 2012 and Google brought it to search (Singhal, 2012). A graph is valuable when the knowledge lives in the connections between facts. It makes the relationships explicit, so they can be followed, checked, corrected and traced back to a source. Until recently, building a graph took a lot of manual curation or purpose-built extraction pipelines. But language models can now extract entities and relationships from text automatically. That has produced graph-based systems for questions about a whole collection of documents (Edge et al., 2024), questions that hop between facts in different documents (Gutiérrez et al., 2024), and facts that change over time, retiring outdated ones (Rasmussen et al., 2025).

None of these is best on its own. Keyword search wins on exact terms, vectors on paraphrases, databases on structured facts and graphs on connections. Side-by-side comparisons of standard and graph-based RAG find that no overall winner exists, with each doing better on the questions it suits (Han et al., 2025; Xiang et al., 2026).

## Look it up: search in agents

The third option is not to store the knowledge at all, but to fetch it when it's needed. Many AI assistants now search the web before answering, especially when the question relates to current events. "Deep research" often runs dozens of searches in a single task, feeding back the results and searching again. Connectors let agents look things up in your email, notes, files and tickets.

Coding agents are a perfect example of leveraging search. Early versions of Claude Code used a local vector database to index and then search the code. What Anthropic found was that allowing for search on the fly with plain text tools like grep usually worked better (Cherny, 2025). The agent doesn't memorise the codebase. It finds its way around it the way an engineer would, by searching for a file name, opening the file and following the references. There is a catch, though. This works because today's models are good enough at deciding what to search for and when to stop.

Search has clear strengths. It is usually current and effectively unlimited, but it also comes with costs.

- **Time and money.** Agentic search typically uses more tokens and takes longer than a single lookup.
- **Too much information.** Pulling in everything relevant can sometimes bury the answer. Long context windows can lead to information being "lost in the middle" (Liu et al., 2024).
- **Trust and governance.** The open web is not a curated source of information, nor is it safe from malicious attempts to target AI agents, such as indirect prompt injection (Greshake et al., 2023). Agents also need rules about what they may access and where data may go.
- **Nothing is kept.** Whatever an agent finds while searching is usually gone when the session ends, so next time it searches again from scratch. Unlike the weights or the notes, search stores nothing. If a finding is worth keeping, something has to write it down.

## Knowing where to look

Knowing where to find something matters as much as knowing it, for people and agents alike. Think of a good pub quiz team. Nobody knows everything, but everyone knows who to turn to for football, who for 80s music and who for geography. The psychologist Daniel Wegner called this transactive memory (Wegner, 1987): in couples and teams, people specialise, and the group works because everyone keeps a rough map of who knows what. Agents rely on the same kind of map. They never see a database or a search engine directly, only a list of tools and sources, each with a short description of what it does or knows, and from that they decide where to look.

The map says where the knowledge is and the price decides where to look. The weights answer instantly and almost for free, but may be stale and can't say where an answer came from. Notes are cheap to read and can be trusted, but someone has to build and maintain them. Search is fresh and nearly unlimited, but slow, costly and only as good as what it finds. Good routing means paying only for what the question needs, taking language and general skills from the weights, your own facts from your notes, and anything that changes faster than you can curate it from search.

Researchers have started to build exactly this. Adaptive-RAG judges how complex a question is and chooses between no retrieval, a single search or several (Jeong et al., 2024). Self-Route lets the model decide whether retrieved snippets are enough or whether it needs the full document, getting close to full long-context quality at a fraction of the cost (Li et al., 2024).

The hard cases are the ones where the sources disagree, such as when the model remembers one thing, the notes say another and the web says a third. A good agent notices the conflict, rather than going with whichever answer arrived first.

## In practice

- **Start simple.** Files and keyword search go further than most people expect. Add vectors, and then graphs, when you can name the questions they will answer better.
- **Use a graph when relationships or provenance matter.** Don't reach for one by default. And let the model help build it. Extract the graph from text, then use the graph to check the model.
- **Search for anything that changes faster than you can curate it.** Keep the source alongside every answer, wherever it came from.

Every agent answers the same question many times a day: do I know this, have I written it down, or should I look it up? People have made that choice for as long as there have been notebooks and libraries, mostly without noticing. Agents have to make it explicitly, and so do the people who build them.

## References

- Cherny, B. (2025). Interviewed in [Claude Code: Anthropic's agent in your terminal](https://www.latent.space/p/claude-code). *Latent Space* podcast, 7 May 2025.
- Clark, A. & Chalmers, D. (1998). [The extended mind](https://doi.org/10.1093/analys/58.1.7). *Analysis* 58(1), 7–19.
- Edge, D. et al. (2024). [From local to global: A graph RAG approach to query-focused summarization](https://arxiv.org/abs/2404.16130). arXiv:2404.16130.
- Greshake, K., Abdelnabi, S., Mishra, S., Endres, C., Holz, T. & Fritz, M. (2023). [Not what you've signed up for: Compromising real-world LLM-integrated applications with indirect prompt injection](https://doi.org/10.1145/3605764.3623985). *AISec '23*, 79–90.
- Gutiérrez, B. J., Shu, Y., Gu, Y., Yasunaga, M. & Su, Y. (2024). [HippoRAG: Neurobiologically inspired long-term memory for large language models](https://arxiv.org/abs/2405.14831). *NeurIPS 2024*.
- Han, H. et al. (2025). [RAG vs. GraphRAG: A systematic evaluation and key insights](https://arxiv.org/abs/2502.11371). arXiv:2502.11371.
- Jeong, S., Baek, J., Cho, S., Hwang, S. J. & Park, J. C. (2024). [Adaptive-RAG: Learning to adapt retrieval-augmented large language models through question complexity](https://arxiv.org/abs/2403.14403). *NAACL 2024*.
- Lewis, P. et al. (2020). [Retrieval-augmented generation for knowledge-intensive NLP tasks](https://arxiv.org/abs/2005.11401). *NeurIPS 2020*.
- Li, Z., Li, C., Zhang, M., Mei, Q. & Bendersky, M. (2024). [Retrieval augmented generation or long-context LLMs? A comprehensive study and hybrid approach](https://arxiv.org/abs/2407.16833). *EMNLP 2024 (Industry Track)*.
- Lindsey, J. et al. (2025). [On the biology of a large language model](https://transformer-circuits.pub/2025/attribution-graphs/biology.html). *Transformer Circuits Thread*, Anthropic, 27 March 2025.
- Liu, N. F., Lin, K., Hewitt, J., Paranjape, A., Bevilacqua, M., Petroni, F. & Liang, P. (2024). [Lost in the middle: How language models use long contexts](https://doi.org/10.1162/tacl_a_00638). *Transactions of the ACL* 12, 157–173.
- Meng, K., Bau, D., Andonian, A. & Belinkov, Y. (2022). [Locating and editing factual associations in GPT](https://arxiv.org/abs/2202.05262). *NeurIPS 2022*.
- Polanyi, M. (1966). *The Tacit Dimension*. Doubleday.
- Quillian, M. R. (1968). Semantic memory. In M. Minsky (ed.), *Semantic Information Processing*, 227–270. MIT Press.
- Rasmussen, P., Paliychuk, P., Beauvais, T., Ryan, J. & Chalef, D. (2025). [Zep: A temporal knowledge graph architecture for agent memory](https://arxiv.org/abs/2501.13956). arXiv:2501.13956.
- Robertson, S. & Zaragoza, H. (2009). [The probabilistic relevance framework: BM25 and beyond](https://doi.org/10.1561/1500000019). *Foundations and Trends in Information Retrieval* 3(4), 333–389.
- Singhal, A. (2012). [Introducing the Knowledge Graph: things, not strings](https://blog.google/products/search/introducing-knowledge-graph-things-not/). *Google blog*, 16 May 2012.
- Wegner, D. M. (1987). Transactive memory: A contemporary analysis of the group mind. In B. Mullen & G. R. Goethals (eds.), *Theories of Group Behavior*, 185–208. Springer.
- Xiang, Z., Wu, C., Zhang, Q., Chen, S., Hong, Z., Huang, X. & Su, J. (2026). [When to use graphs in RAG: A comprehensive analysis for graph retrieval-augmented generation](https://arxiv.org/abs/2506.05690). *ICLR 2026*.
