---
title: "Why We Dream, and Why AI Is Starting To"
description: "Memory, sleep and forgetting."
tags: [memory, agents, neuroscience, llms, continual-learning]
toc: true
---

In 1953 a 27-year-old man called Henry Molaison had brain surgery to stop his seizures. Surgeons removed tissue from deep inside both temporal lobes, including much of the hippocampus on each side. The seizures eased, but from that day until his death in 2008, Henry could not form a lasting memory of new events or facts (Scoville & Milner, 1957). He could hold a conversation, do crosswords and tell stories from his childhood. But leave the room for a few minutes and you came back a stranger.

This might sound familiar. Open a new chat with a language model and you meet something in much the same state: articulate, well-read and with no memory of the last time you spoke. The parallel runs deeper than a simple metaphor. What today's AI systems have, and what they are missing, maps closely onto how the human brain stores, consolidates and forgets. And it has already gone beyond analogy: in the last year, AI agents have started to "dream".

The [first post in this series]({% post_url 2026-09-28-what-does-a-machine-actually-know %}) asked what a machine can be said to know. This one asks how it remembers, and what it should forget.

## Different kinds of memory

H.M. advanced our understanding of memory as much through what he kept as through what he lost. He could hold a number in mind for a few seconds. He remembered much of his early life. And he could still learn skills. In one of Brenda Milner's studies in the early 1960s, he was asked to trace a star while seeing his hand only in a mirror, a task people get better at with practice (Milner, 1962). H.M. got better day after day, while insisting each time that he had never tried it before.

If memory were a single faculty, all of this should have gone together. Instead, one kind of memory had failed and the rest still worked. Psychologists have since mapped out the different types of memory, and nearly every one has a counterpart in today's AI systems.

- **Working memory** holds what you're thinking about right now, like a phone number as you dial it (Baddeley & Hitch, 1974). It is small and fades in seconds. A model's equivalent is its context window, everything it "remembers" from the current conversation, gone when the conversation ends.
- **Semantic memory** holds facts or general knowledge, regardless of when or where you learned it: that Paris is in France, what a dog is (Tulving, 1972). In an LLM, this is baked into the weights, "absorbed" from training data with no record of where any of it came from.
- **Episodic memory** holds what happened to you: last Tuesday's dinner, your first day at school (Tulving, 1972). The closest thing an AI model has is what gets bolted on, such as logs of past conversations that an agent can search and reread.
- **Procedural memory** holds how to do things, like riding a bike or typing (Squire, 2004). For a model, that's the skills (post-)trained into it, such as following instructions or using a tool.

H.M. lost the ability to add new episodic and semantic memories. A chatbot without external memory has almost the same profile, except that it can't pick up new skills either.

## Fast and slow

Why would the brain split memory up like this? The most influential answer came, perhaps, in 1995 from James McClelland, Bruce McNaughton and Randall O'Reilly. The brain, they argued, has two systems that work in tandem.

The first captures experience as it happens: you meet someone once and remember their name. That needs a rapid learner, and in the brain it's the hippocampal system. The second, the neocortex, builds general knowledge from specific experiences, such as what faces look like or how a city is laid out. That needs a slow learner that changes a little with each experience and gradually extracts what experiences have in common.

Why not a single system that builds memories and generalises from experience continuously? Part of the answer came from Michael McCloskey and Neal Cohen in 1989. They found what they called catastrophic interference in networks that store information in the weights of their connections. Such networks have many desirable properties for modelling human cognition, but when they learn tasks one after another, each new one overwrites the last. The same problem is one reason nobody retrains a language model on every new fact. A large model is a slow learner by design, so new information goes in by the fast route instead: pasted into its context, or fetched from a retrieval store at the moment it's needed.

Even the shape of that fast route has a precedent. According to one influential theory, the hippocampus doesn't store the full memory at all, but an index that points to which patterns across the cortex were active together, so a partial cue can bring the whole experience back (Teyler & DiScenna, 1986). Retrieval systems work on a similar principle, a compact index pointing to content kept elsewhere. HippoRAG was built on this theory explicitly (Gutiérrez et al., 2024).

## The bridge between the two systems

If memories start in the fast system and end up in the slow one, how do they get across? Much of the answer seems to be sleep.

In 1994 Matthew Wilson and Bruce McNaughton recorded neurons in the hippocampus of rats performing spatial tasks. Some neurons fire only when the animal is in a particular spot, so as a rat moves, they fire in a sequence that traces its route. When the rats slept afterwards, neurons that had fired together during the task tended to fire together again, as if the brain was replaying the day. Over nights, weeks and years, this replay appears to teach the cortex (Diekelmann & Born, 2010). As evidence, when sharp-wave ripples (brief, intense bursts of hippocampal activity that carry the replay) were suppressed in sleeping rats, the rats learned more slowly (Girardeau et al., 2009). What the cortex ends up holding, though, seems to be mostly the gist. H.M.'s memories from long before the surgery survived, but largely as facts about his life rather than scenes he could relive (Steinvorth, Levine & Corkin, 2005). Consolidation seems to turn episodes into knowledge, losing the detail on the way.

AI research has drawn on the same idea. Replaying stored experience had been used in reinforcement learning since the early 1990s (Lin, 1992), but DeepMind made it famous in 2015 with an agent that learned to play dozens of Atari games at a level comparable to a professional human games tester. One of the keys to making it work was replaying random samples from a store of past moments during training, an idea its authors linked to replay in the hippocampus (Mnih et al., 2015). Without it, learning became unstable, because the agent was learning only from its most recent, closely related experiences.

Others have pushed even closer to biology. Timothy Tadros and colleagues gave a neural network a sleep-like phase after each new task, driven by spontaneous activity rather than stored data, and found it recovered old tasks the network had otherwise forgotten (Tadros et al., 2022). The old memories hadn't been erased, only buried, and sleep dug them back out.

If the sleeping brain is replaying the day, why are dreams so strange? If sleep's job were faithful replay, we would dream reruns. The neuroscientist Erik Hoel offers an answer taken from deep learning (Hoel, 2021). A network trained too closely on its data overfits and performs poorly on anything new. Engineers counter this by adding noise and distortion during training. Dreams, Hoel suggests, do the same job: distorted, recombined versions of the day that stop the brain overfitting to it. It is still a hypothesis, but a telling one.

Deployed language models still have no "night shift", but the agents built on them are starting to get one. Letta, an agent-memory startup, has built "sleep-time" agents that reorganise memory in the background between conversations (Lin et al., 2025). In May 2026 Anthropic previewed a feature for its managed agents called dreaming. That's a scheduled process that reviews past sessions, extracts patterns and curates the agent's memory (Anthropic, 2026). This is a step towards consolidation, but these night shifts don't yet touch the model's weights.

<figure class="figure-wide">
  <div class="figure-wide__scroll"><a href="/assets/images/why-we-dream/fast-and-slow.svg"><img src="/assets/images/why-we-dream/fast-and-slow.svg" width="720" height="340" loading="lazy" alt="Diagram comparing the brain with an AI agent. In the brain, the hippocampus (fast learner) replays experience during sleep into the neocortex (slow learner). In an AI agent, dreaming curates the context and memory store (fast learner), but nothing yet carries what it learns into the model's weights (slow learner)."></a></div>
  <figcaption>Both need a fast learner and a slow one. Sleep carries what the brain learns from the first to the second; an agent's "dreaming" so far only tidies the first.</figcaption>
</figure>

## Forgetting on purpose

Which brings us to the most underrated and perhaps counter-intuitive thing memory does.

In 1942 Jorge Luis Borges wrote "Funes el memorioso", a story about Ireneo Funes, a young man who remembers everything after falling off a horse. He lives in a world made up of countless details and seems incapable of abstraction. Thinking, Borges suggests, means forgetting differences in order to generalise, and Funes can't do it. The neuropsychologist Alexander Luria documented a real-life Funes in the mnemonist Solomon Shereshevsky, who could recall long lists years later but struggled with abstractions (Luria, 1968).

An AI agent whose memory only grows is heading towards Funes. Each retrieval has more to sift through, old and new versions of the same fact compete, and detail crowds out pattern. The brain has three ways to avoid this.

**Forgetting by usefulness.** In 1885 Hermann Ebbinghaus published the first measurements of forgetting, from a limited study he had run on himself. Most of what he learned faded quickly, then the losses slowed, tracing what became known as the forgetting curve. A century later, John Anderson and Lael Schooler showed why the curve has that shape: in newspaper headlines, speech to children and email, the chance that a word will be needed again falls off over time in the same way (Anderson & Schooler, 1991). Forgetting is a bet on what you will need, based on how often and how recently you have needed it. Park et al.'s generative agents (2023) make a version of the same bet, scoring each memory partly by how recently it was used, so stale memories fade from retrieval.

<figure class="figure-wide">
  <div class="figure-wide__scroll"><a href="/assets/images/why-we-dream/forgetting-curve.svg"><img src="/assets/images/why-we-dream/forgetting-curve.svg" width="720" height="390" loading="lazy" alt="Line chart of Ebbinghaus's forgetting curve on a log time scale. Time saved when relearning: 58% after 20 minutes, 44% after 1 hour, 36% after 9 hours, 34% after 1 day, 28% after 2 days, 25% after 6 days and 21% after 31 days."></a></div>
  <figcaption>Ebbinghaus's own data (1885): how much time he saved when relearning lists of nonsense syllables after different delays. Within an hour, more than half the benefit of learning was gone; a month later, about a fifth remained.</figcaption>
</figure>

**Pruning during sleep.** Giulio Tononi and Chiara Cirelli argue that a day of learning strengthens many connections between neurons, and sleep scales them back down. The strongest survive and the weakest fade (Tononi & Cirelli, 2014). This principle closely resembles regularisation in statistical and machine learning, i.e. penalising detail so a model keeps only what generalises. Blake Richards and Paul Frankland proposed that memory exists to aid decision-making in complex environments and not to preserve the past per se. Losing the specifics, i.e. not overfitting, is part of how it does that (Richards & Frankland, 2017).

**Rewriting instead of appending.** Recalling a memory can make it briefly unstable, so it has to be stored again and may change in the process. This was first shown for fear memories in rats (Nader, Schafe & LeDoux, 2000), and how far it extends to everyday human memory is still debated. The brain updates what it knows. Most agent memory today, by contrast, simply appends. Curating memory between sessions through dreaming is an attempt to do it the brain's way.

## In practice

If you're building agents with memory, three simple ideas follow from all this:

- **Give memories a half-life.** Score them by how recently and how often they are used, and let the unused ones fade from retrieval rather than keeping everything equally close at hand.
- **Schedule a night shift.** Periodically distil raw logs into short, general notes, such as a CLAUDE.md file, instead of searching every transcript forever.
- **Update, don't append.** When a new fact contradicts an old one, replace or retire the old entry, and keep a note of where each fact came from.

We have built machines with a long-term memory distilled from tens of trillions of tokens, roughly tens of thousands of reading lifetimes for a person; a short-term memory that can hold all of *War and Peace* at once; notebooks like the CLAUDE.md files developers leave for their coding agents; and, as of this year, something like a night shift. What they don't yet have is a sleep deep enough to change what they know, or a good way to decide what to forget.

## References

- Anderson, J. R. & Schooler, L. J. (1991). [Reflections of the environment in memory](https://doi.org/10.1111/j.1467-9280.1991.tb00174.x). *Psychological Science* 2(6), 396–408.
- Anthropic (2026). [New in Claude Managed Agents: dreaming, outcomes, and multiagent orchestration](https://claude.com/blog/new-in-claude-managed-agents). May 2026.
- Baddeley, A. D. & Hitch, G. (1974). [Working memory](https://doi.org/10.1016/S0079-7421%2808%2960452-1). *Psychology of Learning and Motivation* 8, 47–89.
- Borges, J. L. (1942). "Funes el memorioso" ("Funes the Memorious"). Collected in *Ficciones* (1944).
- Diekelmann, S. & Born, J. (2010). [The memory function of sleep](https://doi.org/10.1038/nrn2762). *Nature Reviews Neuroscience* 11(2), 114–126.
- Ebbinghaus, H. (1885). *Über das Gedächtnis*. Duncker & Humblot.
- Girardeau, G., Benchenane, K., Wiener, S. I., Buzsáki, G. & Zugaro, M. B. (2009). [Selective suppression of hippocampal ripples impairs spatial memory](https://doi.org/10.1038/nn.2384). *Nature Neuroscience* 12(10), 1222–1223.
- Gutiérrez, B. J., Shu, Y., Gu, Y., Yasunaga, M. & Su, Y. (2024). [HippoRAG: Neurobiologically inspired long-term memory for large language models](https://arxiv.org/abs/2405.14831). *NeurIPS 2024*.
- Hoel, E. (2021). [The overfitted brain: Dreams evolved to assist generalization](https://doi.org/10.1016/j.patter.2021.100244). *Patterns* 2(5), 100244.
- Lin, K., Snell, C., Wang, Y., Packer, C., Wooders, S., Stoica, I. & Gonzalez, J. E. (2025). [Sleep-time compute: Beyond inference scaling at test-time](https://arxiv.org/abs/2504.13171). arXiv:2504.13171.
- Lin, L.-J. (1992). [Self-improving reactive agents based on reinforcement learning, planning and teaching](https://doi.org/10.1023/A:1022628806385). *Machine Learning* 8(3–4), 293–321.
- Luria, A. R. (1968). *The Mind of a Mnemonist*. Basic Books.
- McClelland, J. L., McNaughton, B. L. & O'Reilly, R. C. (1995). [Why there are complementary learning systems in the hippocampus and neocortex](https://doi.org/10.1037/0033-295X.102.3.419). *Psychological Review* 102(3), 419–457.
- McCloskey, M. & Cohen, N. J. (1989). [Catastrophic interference in connectionist networks: The sequential learning problem](https://doi.org/10.1016/S0079-7421%2808%2960536-8). *Psychology of Learning and Motivation* 24, 109–165.
- Milner, B. (1962). Les troubles de la mémoire accompagnant des lésions hippocampiques bilatérales. In *Physiologie de l'hippocampe*, 257–272. CNRS.
- Mnih, V. et al. (2015). [Human-level control through deep reinforcement learning](https://doi.org/10.1038/nature14236). *Nature* 518(7540), 529–533.
- Nader, K., Schafe, G. E. & LeDoux, J. E. (2000). [Fear memories require protein synthesis in the amygdala for reconsolidation after retrieval](https://doi.org/10.1038/35021052). *Nature* 406(6797), 722–726.
- Park, J. S. et al. (2023). [Generative agents: Interactive simulacra of human behavior](https://doi.org/10.1145/3586183.3606763). *UIST '23*.
- Richards, B. A. & Frankland, P. W. (2017). [The persistence and transience of memory](https://doi.org/10.1016/j.neuron.2017.04.037). *Neuron* 94(6), 1071–1084.
- Scoville, W. B. & Milner, B. (1957). [Loss of recent memory after bilateral hippocampal lesions](https://doi.org/10.1136/jnnp.20.1.11). *Journal of Neurology, Neurosurgery and Psychiatry* 20(1), 11–21.
- Squire, L. R. (2004). [Memory systems of the brain: A brief history and current perspective](https://doi.org/10.1016/j.nlm.2004.06.005). *Neurobiology of Learning and Memory* 82(3), 171–177.
- Steinvorth, S., Levine, B. & Corkin, S. (2005). [Medial temporal lobe structures are needed to re-experience remote autobiographical memories: Evidence from H.M. and W.R.](https://doi.org/10.1016/j.neuropsychologia.2005.01.001) *Neuropsychologia* 43(4), 479–496.
- Tadros, T., Krishnan, G. P., Ramyaa, R. & Bazhenov, M. (2022). [Sleep-like unsupervised replay reduces catastrophic forgetting in artificial neural networks](https://doi.org/10.1038/s41467-022-34938-7). *Nature Communications* 13, 7742.
- Teyler, T. J. & DiScenna, P. (1986). [The hippocampal memory indexing theory](https://doi.org/10.1037/0735-7044.100.2.147). *Behavioral Neuroscience* 100(2), 147–154.
- Tononi, G. & Cirelli, C. (2014). [Sleep and the price of plasticity](https://doi.org/10.1016/j.neuron.2013.12.025). *Neuron* 81(1), 12–34.
- Tulving, E. (1972). Episodic and semantic memory. In E. Tulving & W. Donaldson (eds.), *Organization of Memory*, 381–403. Academic Press.
- Wilson, M. A. & McNaughton, B. L. (1994). [Reactivation of hippocampal ensemble memories during sleep](https://doi.org/10.1126/science.8036517). *Science* 265(5172), 676–679.
