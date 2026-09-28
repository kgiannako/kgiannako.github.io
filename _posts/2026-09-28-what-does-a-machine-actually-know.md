---
title: "What Does a Machine Actually Know?"
description: "Knowledge, information and memory, from Plato to AI agents."
tags: [llms, retrieval, memory, epistemology, information-theory]
toc: true
---

In 2023 two New York lawyers filed a brief citing six court cases that did not exist. ChatGPT had supplied them, complete with plausible names, citations and quotations, and when asked whether they were real, it said they were. The lawyers and their firm were fined $5,000 (*Mata v. Avianca*, S.D.N.Y. 2023).

It is tempting to call this lying, or a bug. But the episode raises harder questions. Did the model know the law and garble it, or did it never know anything? Where, among billions of parameters, would that knowledge even live? And were those fake citations information, or only something shaped like it?

Each of these is a question about knowledge, information or memory, and each is far older than computing. Philosophers have argued over them for more than two thousand years, engineers and neuroscientists for the last hundred, and their answers explain a surprising amount about the systems we are building now. This post is a first pass through all three.

## What is it to know?

In the *Theaetetus*, Plato has Socrates ask what knowledge, ἐπιστήμη (*epistēmē*), actually is. The dialogue's most promising answer is true belief with an account: a true δόξα (*doxa*, belief) backed by λόγος (*logos*, a reason or explanation). A belief can be right by accident. The account is what connects it to why it is right. Socrates ends up rejecting even this, and the dialogue closes without a definition. But the idea stuck.

By that standard, the fake citations were not a failure of knowledge so much as its absence. The model produced something that looked exactly like a legal belief, fluent and specific, with no account behind it. Nothing connected the output to a court record.

In the *Meno*, Socrates explains why the account matters. True beliefs, he says, are like the statues of Daedalus, which were said to walk off unless tied down. A belief tied down by reasoning about its cause stays put, and that is knowledge. This is, more or less, the case for making models cite their sources. A citation you can check is the rope.

A version of this idea, knowledge as justified true belief, became the textbook definition, until Edmund Gettier broke it in a three-page paper in 1963. He showed you can hold a justified, true belief and still be right only by luck. Bertrand Russell had already given the neatest example in 1948. You look at a clock that stopped exactly twelve hours ago. It shows the right time, you have every reason to trust it, and you still don't know the time.

Every language model is Russell's clock. Its training data stops at a cutoff date. Ask who is the UK prime minister today and, if nothing has changed since the cutoff, it answers correctly, but only by luck. If something has changed, it is wrong in exactly the same confident voice. From the outside the two look identical, which is why a high benchmark score is not the same as knowledge.

There is a second distinction. Gilbert Ryle separated *knowing that* (Paris is the capital of France) from *knowing how* (riding a bike). Michael Polanyi observed that "we can know more than we can tell": much real expertise can't be put into words. A language model is an extreme case of this tacit knowledge. It can do a great deal, but ask how it knows and the explanation it gives is generated fresh, not read off from wherever the answer came from. Knowledge graphs make the opposite bet: every fact is an explicit statement that can be traced back to its source. Much of current AI engineering is an attempt to get the fluency of the first with the accountability of the second.

## A measure of surprise

Oddly, the systems we call AI are built on a theory that deliberately ignores meaning.

In 1948 Claude Shannon defined information as the reduction of uncertainty. A message is informative to the degree that it surprises you, and that surprise can be measured in bits. He was explicit that what a message means is irrelevant to the engineering problem of sending it. That decision made information measurable, and the digital world followed.

Seventy-odd years later, the same quantity sits at the heart of every language model. Training means asking the model to predict the next word and penalising it by how surprised it was by the real one. The loss function is essentially Shannon's measure. A model trained this way becomes very good at producing unsurprising text: text that looks like what usually comes next. The fake citations are what that looks like when it goes wrong, exactly the right shape with nothing underneath.

Warren Weaver saw the gap in 1949. He split communication into three problems. Can the symbols be transmitted accurately? Do they convey the intended meaning? Do they have the intended effect? Shannon's theory addressed only the first. The argument over whether language models understand anything, whether they are "stochastic parrots" (Bender et al., 2021) or build real models of the world, is an argument over whether they reach Weaver's second level. Gregory Bateson's later definition of information, "a difference which makes a difference", is a reminder of what the first level leaves out.

Three years before Shannon, Vannevar Bush had imagined a different kind of machine. In "As We May Think" (1945) he described the memex, a desk that stores its owner's books, records and correspondence and links items by associative trails: a mechanical extension of memory. It is a fair description of what retrieval-augmented AI systems do today. They store documents, find the ones related to a question and hand them to the model. Bush's most lasting idea was a machine that remembers for us rather than one that thinks for us.

## Where does a model keep what it knows?

Plato compared memory to a block of wax in the mind, where experiences leave impressions, some sharp and some smudged. A few pages later he tried a second image: memory as an aviary. We own the birds we have caught, but to use one we have to reach in and grab it, and sometimes we grab the wrong bird. Owning knowledge and having it in hand are different things.

Language models make this distinction concrete. What a model learned in training is stored in its weights: owned, but not in hand. What it is working with right now sits in its context window. Much of practical AI engineering is about getting the right bird out of the aviary and into the hand.

Aristotle went further. He separated μνήμη (*mnēmē*), holding an image of the past, from ἀνάμνησις (*anamnēsis*), the act of searching for it, and noticed that the search moves by association: from one thing to something similar, opposite or nearby. Modern retrieval systems search in much the same way, looking for items that sit close together in a space of meanings.

The science of memory adds three findings that map onto AI with some precision.

- **Memory is reconstructed, not replayed.** In *Remembering* (1932), Frederic Bartlett described asking people to retell an unfamiliar folk tale. They reshaped it to fit what they expected, dropping odd details and inventing familiar ones. The fake citations are Bartlett's finding in a machine. The model rebuilt what a legal citation usually looks like instead of retrieving one.
- **Memory is several systems, and one can fail on its own.** After surgery in 1953 removed much of the hippocampus on both sides of his brain, the patient known as H.M. could no longer form new memories of facts or events, yet he could still learn new motor skills. A language model without external memory is in a similar position. Everything it knows was laid down before training ended, and each conversation is forgotten when it closes.
- **The storage is hard to find.** In 1950 Karl Lashley summed up decades of searching for the physical trace of a memory, the engram, and concluded it wasn't in any one place. Interpretability researchers now run the same search inside neural networks, locating and even editing individual facts in a model's weights (Meng et al., 2022).

One more idea ties these together. McClelland, McNaughton and O'Reilly (1995) argued that the brain needs two learning systems: a fast one that records episodes as they happen, and a slow one that gradually absorbs general structure. A single system that learned fast would overwrite what it already knew, a problem machine-learning researchers call catastrophic forgetting. Language models have the slow system in their weights. The fast one is what engineers are now building around them.

## A notebook and a mind

In 1998 the philosophers Andy Clark and David Chalmers proposed a thought experiment. Otto has Alzheimer's and carries a notebook everywhere. When he wants to visit a museum, he looks up the address instead of remembering it. If the notebook does the job memory does for everyone else, they argued, then it is part of Otto's mind. The mind doesn't have to stop at the skull.

AI agents are built on the same idea. A model's own memory is frozen when training ends, so we give it notebooks: documents it can retrieve, knowledge graphs it can query, and running logs it can write to and reflect on. Some designs borrow directly from the science above. The CoALA framework (Sumers et al., 2024) sorts agent memory into working, episodic, semantic and procedural, the categories psychologists settled on decades ago. HippoRAG (Gutiérrez et al., 2024) models its retrieval on the hippocampus.

This is where the three ideas meet. Knowledge asks what makes an answer trustworthy. Information asks what separates a meaningful answer from a merely well-formed one. Memory asks where the answer is kept and how it is found. For an AI agent these are no longer separate questions. They are one design problem: what to store, how to find it, and how to tell a belief tied to a source from one that only sounds right.

The rest of this series is about how to tie the statues down.

## References

- Plato, *Theaetetus* (wax block 191c; aviary 197c; true belief with an account 201c) and *Meno* (statues of Daedalus 97d–98a). Aristotle, *On Memory and Recollection* (recollection by association 451b).
- Bartlett, F. C. (1932). *Remembering: A Study in Experimental and Social Psychology*. Cambridge University Press.
- Bateson, G. (1972). *Steps to an Ecology of Mind*. Chandler.
- Bender, E. M., Gebru, T., McMillan-Major, A. & Shmitchell, S. (2021). [On the dangers of stochastic parrots: Can language models be too big?](https://doi.org/10.1145/3442188.3445922) *FAccT '21*, 610–623.
- Bush, V. (1945). [As we may think](https://www.theatlantic.com/magazine/archive/1945/07/as-we-may-think/303881/). *The Atlantic*, July 1945.
- Clark, A. & Chalmers, D. (1998). [The extended mind](https://doi.org/10.1093/analys/58.1.7). *Analysis* 58(1), 7–19.
- Corkin, S. (1968). [Acquisition of motor skill after bilateral medial temporal-lobe excision](https://doi.org/10.1016/0028-3932%2868%2990024-9). *Neuropsychologia* 6(3), 255–265.
- Gettier, E. (1963). [Is justified true belief knowledge?](https://doi.org/10.1093/analys/23.6.121) *Analysis* 23(6), 121–123.
- Gutiérrez, B. J., Shu, Y., Gu, Y., Yasunaga, M. & Su, Y. (2024). [HippoRAG: Neurobiologically inspired long-term memory for large language models](https://arxiv.org/abs/2405.14831). *NeurIPS 2024*.
- Lashley, K. S. (1950). In search of the engram. *Symposia of the Society for Experimental Biology* 4, 454–482.
- *Mata v. Avianca, Inc.*, 678 F. Supp. 3d 443, No. 22-cv-1461 (PKC) (S.D.N.Y. June 22, 2023).
- McClelland, J. L., McNaughton, B. L. & O'Reilly, R. C. (1995). [Why there are complementary learning systems in the hippocampus and neocortex](https://doi.org/10.1037/0033-295X.102.3.419). *Psychological Review* 102(3), 419–457.
- Meng, K., Bau, D., Andonian, A. & Belinkov, Y. (2022). [Locating and editing factual associations in GPT](https://arxiv.org/abs/2202.05262). *NeurIPS 2022*.
- Polanyi, M. (1966). *The Tacit Dimension*. Doubleday.
- Russell, B. (1948). *Human Knowledge: Its Scope and Limits*. George Allen & Unwin.
- Ryle, G. (1949). *The Concept of Mind*. Hutchinson.
- Scoville, W. B. & Milner, B. (1957). [Loss of recent memory after bilateral hippocampal lesions](https://doi.org/10.1136/jnnp.20.1.11). *Journal of Neurology, Neurosurgery and Psychiatry* 20(1), 11–21.
- Shannon, C. E. (1948). [A mathematical theory of communication](https://doi.org/10.1002/j.1538-7305.1948.tb01338.x). *Bell System Technical Journal* 27(3), 379–423 and 27(4), 623–656.
- Shannon, C. E. & Weaver, W. (1949). *The Mathematical Theory of Communication*. University of Illinois Press.
- Sumers, T. R., Yao, S., Narasimhan, K. & Griffiths, T. L. (2024). [Cognitive architectures for language agents](https://arxiv.org/abs/2309.02427). *Transactions on Machine Learning Research*.
