---
title: "Reasoning in Minds and Machines"
description: "AI reasons more like us than we might expect, for better and for worse."
tags: [reasoning, llms, agents, cognition, mathematics]
toc: true
---

Ask a modern AI model a question like "how many times does the digit 7 appear if you write out every number from 1 to 1,000?", and it won't answer straight away. First it writes, sometimes pages of working, counting the units, then the tens, then the hundreds, checking whether 77 counts once or twice, spotting a slip: "Wait, 777 has three sevens, not one. Let me recount." Then a short, confident answer, 300. In 2022, researchers showed that asking for step-by-step working improved answers. OpenAI built it into a commercial product with o1 in 2024, and today most leading models offer some version of it, usually as a switch or a dial for how hard to think.

Reading these traces is quite remarkable and a bit bizarre at times. They look a lot like someone thinking on paper, like an inner monologue. The question is whether this is reasoning or a very good imitation of it. A less obvious question is whether it really matters.

## What we mean by reasoning

The philosopher Charles Sanders Peirce, writing from the 1870s onwards, split reasoning into three kinds. You come home to find the kitchen floor wet. Your first thought is that the dishwasher has leaked again. That is abduction, a guess at the best explanation for something surprising. Then you look more closely. The water is pooling under the dishwasher, the floor by the sink is dry, and nothing else in that corner carries water, so it must be the dishwasher. That is deduction. If the premises are true, the conclusion has to be. Finally, you remember it has leaked three times this year, each time after the long eco cycle, and conclude that the long cycle is the problem. That is induction, a general rule drawn from repeated cases.

Only deduction guarantees its conclusion. Guesses and generalisations can be wrong, yet most everyday reasoning runs on abduction and induction, from a doctor reading symptoms to a scientist proposing a theory. Language models, trained to produce the most plausible continuation of a text, are arguably natural guessers. The harder question is whether they can reliably deduce and generalise as well.

Psychology adds a second dimension, speed. Daniel Kahneman described two modes of thinking. System 1 is fast, automatic and intuitive, and System 2 is slow, deliberate and effortful. A quick demo of the two systems is a puzzle from Shane Frederick's Cognitive Reflection Test. "A bat and a ball cost £1.10 together, and the bat costs £1 more than the ball. How much is the ball?" Most people's first answer is 10p. It feels right and it is wrong. Stop and check, and a 10p ball would make the bat £1.10 and the total £1.20. The ball costs 5p. [Post 2]({% post_url 2026-10-04-why-we-dream-and-why-ai-is-starting-to %}) described memory working at two speeds, and reasoning has two speeds as well. A plain LLM is close to pure System 1. It writes one token at a time, and each token gets the same fixed amount of computation whether the question is trivial or not. Thinking modes are, in effect, an attempt to give it a System 2.

Slowing down helps, but even a human System 2 is not a clean logic engine. How well people reason depends a great deal on what the problem is about. In the best-known version of Peter Wason's selection task (first published in 1966), people see four cards showing E, K, 4 and 7, and are told every card has a letter on one side and a number on the other. The rule to test is "if a card has a vowel on one side, it has an even number on the other". Which cards must be turned over? Most people choose E and 4. The right answer is E and 7, since only a vowel behind the 7 could break the rule. In Wason's own studies fewer than one person in ten got it right. Yet when the same logic is dressed as a social rule ("if someone is drinking beer, they must be over 19"), most people solve it at once (Griggs & Cox, 1982). Human reasoning depends heavily on content and familiarity, not just on logical form.

Hugo Mercier and Dan Sperber reject the two-systems picture altogether. In *The Enigma of Reason* (2017) they argue that reason is not a separate, slower faculty that corrects intuition, but one more intuitive ability, specialised in judging which reasons support which conclusions. Its main job, on their account, is social: it evolved mainly to produce arguments that persuade others and to evaluate the arguments others make, rather than to find the truth on one's own. That would explain why people are good at poking holes in other people's arguments, lazy about their own, and reason better in groups. It also suggests that reasons are often produced after the fact, to justify a conclusion already reached.

For what follows, it's good to have a working definition of reasoning. Reasoning is using what we know, together with new information, to assess a situation, make a decision, solve a problem or reach a new conclusion, one step at a time, in steps that can be checked and corrected. Recent research has tried to give machines that ability in at least four different ways.

## Reasoning in words

The first and most visible way is to let the model write its working down. In 2022, Jason Wei and colleagues at Google showed that adding a few worked examples with written-out steps to a prompt sharply improved large models on arithmetic and symbolic reasoning. They called it chain-of-thought prompting. The same year, Takeshi Kojima and colleagues found that simply appending "Let's think step by step" had a similar, if usually smaller, effect.

But why should writing things down help a machine? One plausible explanation is that a model cannot think longer about a hard token than an easy one, but it can produce more tokens. Each written step becomes input to the next, so the text effectively works as a scratchpad. Much of the computation can happen in the working itself.

Many refinements followed quickly. Self-consistency (Wang et al., 2022) samples many reasoning paths for the same question and takes a majority vote over the answers, on the basis that there are many ways to be wrong but the right answer tends to recur. Tree of Thoughts (Yao et al., 2023) lets the model branch, evaluate partial solutions and backtrack, closer to how a person explores a puzzle. On the Game of 24, where four numbers must be combined into 24, GPT-4 with plain chain-of-thought solved 4% of the test problems and with Tree of Thoughts 74%.

Eventually, the reasoning moved from the prompt into training. OpenAI's o1 (September 2024) was trained with reinforcement learning to produce long internal chains of thought before answering. DeepSeek-R1 followed shortly after (January 2025), making its recipe public: reward the model mainly for correct final answers on maths and coding problems, and let it work out how to get there. Interesting behaviours emerged during training, such as rechecking, trying alternatives and abandoning dead ends.

These models also introduced a new way to improve performance, often called test-time compute. OpenAI reported that o1 got better both with more training and with more time to think on each question, so letting a model think longer can make it more accurate. But longer thinking also means slower answers and many more tokens, and models sometimes overthink simple questions that need little or no reasoning.

## Reasoning with tools

For some kinds of thinking, like exact arithmetic, words are a poor medium. Language models were notoriously unreliable at multiplying large numbers (Dziri et al., 2023), partly because without written working there is nowhere to hold the intermediate results, much like trying to multiply two six-digit numbers in your head. Reasoning models have since improved a great deal, and like people, they do best with the right tools, such as a calculator.

Program-aided language models (Gao et al., 2022) and Program of Thoughts (Chen et al., 2022) aimed to separate the reasoning from the computation by asking the model to write its reasoning as a short program. The model decides what to compute, then a Python interpreter does the computing. On maths word problems this beat chain-of-thought, mostly by removing arithmetic slips. ReAct (Yao et al., 2022) took a broader route, interleaving thoughts with actions such as a search or a lookup, then reading the result before the next thought. Reason, act, observe, repeat. Most agents today still run on some version of that loop, and agent frameworks such as LangGraph are built around it.

Handing work to tools echoes the extended mind from [Post 1]({% post_url 2026-09-28-what-does-a-machine-actually-know %}) and [Post 3]({% post_url 2026-10-18-where-does-an-ai-keep-what-it-knows %}). Andy Clark and David Chalmers argued that a notebook can be part of someone's memory, and by the same logic a calculator or a Python interpreter can be part of someone's reasoning. Knowing when to reach for the tool is itself part of reasoning well, for people and for models.

## Reasoning in formal languages

The idea that reasoning is, or can be turned into, calculation is old. Thomas Hobbes wrote in *Leviathan* (1651) that reason "is nothing but reckoning". Gottfried Leibniz later imagined a formal language in which disputes could be settled by saying "let us calculate". George Boole's *The Laws of Thought* (1854) turned logic into algebra. By the 20th century proofs could be written in systems that a machine could, in principle, check line by line.

The idea also met its limits. In 1931 Kurt Gödel showed that any consistent formal system powerful enough to express arithmetic contains true statements it cannot prove, so no single system can capture all of mathematics. The more practical bottleneck is that a problem has to be stated formally first, while real problems arrive in messy language.

This is where language models help. They are good at fuzzy translation but weak at rigid checking, while solvers and proof checkers are the opposite, so combining the two plays to the strengths of each.

Logic-LM (Pan et al., 2023) is a simple version of the idea. The model translates a word problem into symbolic form, an off-the-shelf solver works out the answer, and any error from the solver goes back to the model to fix its translation. On logical reasoning benchmarks it beat chain-of-thought alone.

Google DeepMind applied the same split to olympiad mathematics. In AlphaGeometry (Trinh et al., 2024), a symbolic engine does the deductions, and when it gets stuck a language model suggests the creative move, an extra point or line, so the engine can carry on. It solved 25 of 30 past olympiad geometry problems, close to the average human gold medallist. AlphaProof went further, into Lean, a language in which every step of a proof is checked by a small, trusted program, so a proof either compiles or it does not. At the 2024 International Mathematical Olympiad the two systems together reached silver-medal standard, although humans first translated the problems into Lean by hand and some solutions took days.

At the 2025 Olympiad, a version of Gemini called Deep Think reached gold-medal standard writing its proofs in ordinary English, within the time limit, and its results were certified by the competition's coordinators. OpenAI reported a gold-level result too, graded by former medallists rather than officially.

In 2026 the two strands met at research level. In September, OpenAI announced that a large team of AI agents had produced a proof that the Navier–Stokes equations, which describe how fluids flow, can blow up in finite time when a smooth external force is applied. OpenAI argues this settles one of the Clay Millennium Prize Problems, and it published a Lean formalisation alongside. A month later it released more than 700 AI-written mathematical manuscripts, only some of them with Lean proofs at launch. Both are still being checked. The Clay Institute will recognise a solution only after peer review, and an October preprint by Bastounis, Circelli and Hansen argues that the Navier–Stokes Lean proof does not correspond to the written one.

A Lean proof can be verified by a small, trusted program, while a natural-language proof has to be read and judged by experts. But a machine check only confirms that the formal statement was proved, not that it is the statement anyone cared about. As models write longer and more ambitious arguments, in mathematics, software or law, the gap between reasoning that can be verified and reasoning that only looks right becomes the central question.

## Reasoning without words

The fourth approach goes the other way, away from text altogether. Writing every step as a word forces the model's rich internal state through a narrow channel. At each step it must commit to one token and discard everything else it was considering.

Coconut, short for Chain of Continuous Thought (Hao et al., 2024, from Meta), feeds the last internal state straight back in as the next input and keeps going, instead of turning it into a word. The researchers found that one of these continuous thoughts can hold several candidate next steps at once, so the model can explore alternatives in parallel, something like a breadth-first search, instead of committing to a single path. On logic problems that require planning ahead, it beat chain-of-thought while generating far fewer tokens. On maths word problems, though, it still trailed chain-of-thought. A related line of work (Geiping et al., 2025) builds models that can loop through the same internal layers more times when a problem is harder, thinking longer without writing anything down.

The drawback is that when the reasoning happens inside the model's internal states, nobody can read it. Chain-of-thought at least gives people something to inspect and possibly correct, whereas latent reasoning gives up even that.

Latent reasoning also revives an old question. Does reasoning need language at all? Jerry Fodor argued that thought runs on its own internal "language of thought", which is not English or any spoken language. From a neuroscience perspective, Evelina Fedorenko and colleagues have shown that the brain's language network stays largely quiet during arithmetic, logic and many other kinds of problem solving, and that some people who have lost most of their language after a stroke can still reason about numbers and logic (Fedorenko et al., 2024). People also differ widely in how much inner speech they report (Hurlburt et al., 2013; Nedergaard & Lupyan, 2024). Some say they hardly hear an inner voice at all. For humans, words seem to be one tool for thinking, not the thinking itself. Machines may turn out the same way.

## Reasons after the fact

If a model writes out its reasoning, it is tempting to treat that text as a window into what it is doing. There is good evidence that the window doesn't show everything.

Miles Turpin and colleagues (2023) gave models a series of multiple-choice examples in which the correct answer always happened to be (A). The models picked up the pattern and started choosing (A) on new questions, then wrote plausible step-by-step explanations for their choices that never mentioned the pattern. In 2025 a team at Anthropic, led by Yanda Chen, slipped hints into prompts and checked whether reasoning models admitted using them. Most of the time they did not. The omissions were not about keeping things short, since the unfaithful explanations were actually longer than the honest ones, and they became more common as questions got harder. In both studies, the written reasoning was plausible but left out what actually drove the answer. The Anthropic team's conclusion was that monitoring a model's reasoning is a promising way to catch unwanted behaviour during training and testing, but not enough on its own to rule it out.

People, too, routinely give plausible reasons that were not the real cause of their choices. In a famous 1977 study, Richard Nisbett and Timothy Wilson asked shoppers to pick the best of four identical pairs of stockings. The pair on the far right was chosen about four times as often as the pair on the far left, and people explained their choice by the quality of the fabric. Nobody mentioned position. Later studies on "choice blindness" (Johansson, Hall and colleagues, 2005) went further. People secretly handed the option they had rejected often didn't notice, and defended it with reasons as if they had chosen it. Mercier and Sperber would not be surprised. If reasoning evolved partly to justify, then a fluent justification is no proof that it caused the decision, in people or in machines.

That's not to say that visible reasoning is useless. Even an imperfect trace often reveals mistakes.

## What counts as reasoning

Nature offers some useful test cases. In 2000, Toshiyuki Nakagaki and colleagues put a slime mould, a single-celled organism with no brain, in a maze with food at two exits. It spread through every corridor, then pulled back from the dead ends until a single tube traced the shortest path. The result looks like reasoning, but the slime mould has no map of the maze. The shortest path simply falls out of the physics of growth and retreat.

In experiments by Alex Taylor and colleagues (2010), New Caledonian crows pulled up a string to get a short stick, used it to fish a longer stick out of a box, then used that to reach food. Birds that already knew each step separately chained all three on their first try. They seem to hold a goal, plan intermediate steps and adjust when something fails.

That suggests three rough tests. Reasoning works through intermediate states that stand for the problem, rather than a physical process that happens to end in the right place. It is flexible, so the same ability carries over when the problem looks different. And it corrects itself, noticing when a step has gone wrong.

Flexibility is where language models struggle most. Apple researchers (Mirzadeh et al., 2024) tested a range of language models on a standard set of school maths problems, changing only the names and numbers. Accuracy varied noticeably and fell for many models, especially when the numbers changed. Adding one irrelevant sentence that had no bearing on the answer caused drops of up to 65%. Another Apple study, *The Illusion of Thinking* (Shojaee et al., 2025), gave reasoning models puzzles like the Tower of Hanoi at increasing sizes and found accuracy collapsing beyond a certain complexity, even when the models were handed the solution algorithm, and the models' reasoning effort actually fell as problems got harder. Critics quickly replied that some failures came from output length limits and from puzzle instances that had no solution (Lawsen, 2025), and the debate is not settled. Behind all of this sits John Searle's Chinese Room (1980). A person following rules to manipulate Chinese characters could produce perfect answers without understanding a word. Producing the right symbols, the argument goes, is not the same as thinking.

Many of the failures in AI have human versions. People fail the Wason task, are swayed by irrelevant numbers (anchoring) and give up on long, tedious problems. Human expertise also leans heavily on pattern recognition. Chess masters, studied by William Chase and Herbert Simon in 1973, recall real board positions far better than novices but lose the advantage when pieces are placed at random. Their skill is built on recognised patterns, yet nobody concludes that chess masters do not reason.

Reasoning is probably better understood as a matter of degree. "Pattern matching or real reasoning?" is the wrong question. Everything that reasons, from crows to chess masters to language models, combines recognition with step-by-step work in some way. The more interesting question is robustness. Does the ability hold when the surface of a problem changes, when the problem gets longer, when nobody is checking? Today's models are remarkable on some problems and a bit hit-and-miss on others that look easy.

## In practice

- **Ask for steps when the problem has steps.** Multi-step maths, planning and logic benefit from reasoning modes; simple lookups and short factual questions mostly pay extra cost and wait for nothing. On simple puzzles, standard models can match or beat reasoning models, and on some tasks thinking longer even makes answers worse (Liu et al., 2024; Shojaee et al., 2025; Gema et al., 2025).
- **Treat visible reasoning as evidence, not proof.** A trace is useful for spotting mistakes, but it may leave out what actually drove the answer.
- **Test on variations.** Before relying on a model for a class of problems, change names, numbers and wording, and add irrelevant details. If the answers change, the reasoning was shallower than it looked.

## So, does it matter?

Does it matter whether machines really reason? Probably less than it first seems. What matters is whether their reasoning holds up when a problem changes, and whether it can be checked. Machines that write out their reasoning were meant to make AI more transparent, and in part they have. But their traces can be fluent, plausible and beside the point, and so can ours.

## References

- Bastounis, A., Circelli, F. & Hansen, A. C. (2026). [Navier–Stokes lost in translation: Why Lean verification of AI autoformalisation does not guarantee correct natural language proofs](https://arxiv.org/abs/2610.08144). arXiv:2610.08144.
- Boole, G. (1854). *An Investigation of the Laws of Thought*. Walton and Maberly.
- Chase, W. G. & Simon, H. A. (1973). [Perception in chess](https://doi.org/10.1016/0010-0285%2873%2990004-2). *Cognitive Psychology* 4(1), 55–81.
- Chen, W., Ma, X., Wang, X. & Cohen, W. W. (2022). [Program of thoughts prompting: Disentangling computation from reasoning for numerical reasoning tasks](https://arxiv.org/abs/2211.12588). arXiv:2211.12588; *TMLR 2023*.
- Chen, Y. et al. (2025). [Reasoning models don't always say what they think](https://arxiv.org/abs/2505.05410). Anthropic. arXiv:2505.05410.
- Clark, A. & Chalmers, D. (1998). [The extended mind](https://doi.org/10.1093/analys/58.1.7). *Analysis* 58(1), 7–19.
- DeepSeek-AI (2025). [DeepSeek-R1 incentivizes reasoning in LLMs through reinforcement learning](https://doi.org/10.1038/s41586-025-09422-z). *Nature* 645, 633–638. First released as arXiv:2501.12948, January 2025.
- Dziri, N. et al. (2023). [Faith and fate: Limits of transformers on compositionality](https://arxiv.org/abs/2305.18654). *NeurIPS 2023*.
- Fedorenko, E., Piantadosi, S. T. & Gibson, E. A. F. (2024). [Language is primarily a tool for communication rather than thought](https://doi.org/10.1038/s41586-024-07522-w). *Nature* 630, 575–586.
- Fodor, J. A. (1975). *The Language of Thought*. Harvard University Press.
- Frederick, S. (2005). [Cognitive reflection and decision making](https://doi.org/10.1257/089533005775196732). *Journal of Economic Perspectives* 19(4), 25–42.
- Gao, L. et al. (2022). [PAL: Program-aided language models](https://arxiv.org/abs/2211.10435). arXiv:2211.10435; *ICML 2023*.
- Geiping, J. et al. (2025). [Scaling up test-time compute with latent reasoning: A recurrent depth approach](https://arxiv.org/abs/2502.05171). arXiv:2502.05171.
- Gema, A. P. et al. (2025). [Inverse scaling in test-time compute](https://arxiv.org/abs/2507.14417). *TMLR*.
- Gödel, K. (1931). [Über formal unentscheidbare Sätze der Principia Mathematica und verwandter Systeme I](https://doi.org/10.1007/BF01700692). *Monatshefte für Mathematik und Physik* 38, 173–198.
- Google DeepMind (2024). [AI achieves silver-medal standard solving International Mathematical Olympiad problems](https://deepmind.google/discover/blog/ai-solves-imo-problems-at-silver-medal-level/). Blog, 25 July 2024.
- Google DeepMind (2025). [Advanced version of Gemini with Deep Think officially achieves gold-medal standard at the International Mathematical Olympiad](https://deepmind.google/discover/blog/advanced-version-of-gemini-with-deep-think-officially-achieves-gold-medal-standard-at-the-international-mathematical-olympiad/). Blog, July 2025.
- Griggs, R. A. & Cox, J. R. (1982). [The elusive thematic-materials effect in Wason's selection task](https://doi.org/10.1111/j.2044-8295.1982.tb01823.x). *British Journal of Psychology* 73(3), 407–420.
- Hao, S., Sukhbaatar, S., Su, D., Li, X., Hu, Z., Weston, J. & Tian, Y. (2024). [Training large language models to reason in a continuous latent space](https://arxiv.org/abs/2412.06769). arXiv:2412.06769; *COLM 2025*.
- Hobbes, T. (1651). *Leviathan*, Part I, Chapter 5.
- Hurlburt, R. T., Heavey, C. L. & Kelsey, J. M. (2013). [Toward a phenomenology of inner speaking](https://doi.org/10.1016/j.concog.2013.10.003). *Consciousness and Cognition* 22(4), 1477–1494.
- Johansson, P., Hall, L., Sikström, S. & Olsson, A. (2005). [Failure to detect mismatches between intention and outcome in a simple decision task](https://doi.org/10.1126/science.1111709). *Science* 310(5745), 116–119.
- Kahneman, D. (2011). *Thinking, Fast and Slow*. Farrar, Straus and Giroux.
- Kojima, T., Gu, S. S., Reid, M., Matsuo, Y. & Iwasawa, Y. (2022). [Large language models are zero-shot reasoners](https://arxiv.org/abs/2205.11916). *NeurIPS 2022*.
- Lawsen, A. (2025). [Comment on The Illusion of Thinking](https://arxiv.org/abs/2506.09250). arXiv:2506.09250.
- Leibniz, G. W. (1685). The art of discovery. In P. P. Wiener (ed.), *Leibniz: Selections* (1951). Charles Scribner's Sons.
- Liu, R., Geng, J., Wu, A. J., Sucholutsky, I., Lombrozo, T. & Griffiths, T. L. (2024). [Mind your step (by step): Chain-of-thought can reduce performance on tasks where thinking makes humans worse](https://arxiv.org/abs/2410.21333). arXiv:2410.21333; *ICML 2025*.
- Mercier, H. & Sperber, D. (2017). *The Enigma of Reason*. Harvard University Press.
- Mirzadeh, I. et al. (2024). [GSM-Symbolic: Understanding the limitations of mathematical reasoning in large language models](https://arxiv.org/abs/2410.05229). arXiv:2410.05229; *ICLR 2025*.
- Nakagaki, T., Yamada, H. & Tóth, Á. (2000). [Maze-solving by an amoeboid organism](https://doi.org/10.1038/35035159). *Nature* 407, 470.
- Nedergaard, J. S. K. & Lupyan, G. (2024). [Not everybody has an inner voice: Behavioral consequences of anendophasia](https://doi.org/10.1177/09567976241243004). *Psychological Science* 35(7), 780–797.
- Nisbett, R. E. & Wilson, T. D. (1977). [Telling more than we can know: Verbal reports on mental processes](https://doi.org/10.1037/0033-295X.84.3.231). *Psychological Review* 84(3), 231–259.
- OpenAI (2024). [Learning to reason with LLMs](https://openai.com/index/learning-to-reason-with-llms/). Blog, 12 September 2024.
- OpenAI (2026). [On the Navier–Stokes Millennium Prize Problem](https://openai.com/index/navier-stokes-solution/). 8 September 2026.
- OpenAI (2026). [openai/math](https://github.com/openai/math). GitHub repository, 6 October 2026.
- Pan, L., Albalak, A., Wang, X. & Wang, W. Y. (2023). [Logic-LM: Empowering large language models with symbolic solvers for faithful logical reasoning](https://arxiv.org/abs/2305.12295). *Findings of EMNLP 2023*.
- Peirce, C. S. (1878). Deduction, induction, and hypothesis. *Popular Science Monthly* 13, 470–482.
- Searle, J. R. (1980). [Minds, brains, and programs](https://doi.org/10.1017/S0140525X00005756). *Behavioral and Brain Sciences* 3(3), 417–424.
- Shojaee, P. et al. (2025). [The illusion of thinking: Understanding the strengths and limitations of reasoning models via the lens of problem complexity](https://arxiv.org/abs/2506.06941). arXiv:2506.06941; *NeurIPS 2025*.
- Taylor, A. H., Elliffe, D., Hunt, G. R. & Gray, R. D. (2010). [Complex cognition and behavioural innovation in New Caledonian crows](https://doi.org/10.1098/rspb.2010.0285). *Proceedings of the Royal Society B* 277(1694), 2637–2643.
- Trinh, T. H., Wu, Y., Le, Q. V., He, H. & Luong, T. (2024). [Solving olympiad geometry without human demonstrations](https://doi.org/10.1038/s41586-023-06747-5). *Nature* 625, 476–482.
- Turpin, M., Michael, J., Perez, E. & Bowman, S. R. (2023). [Language models don't always say what they think: Unfaithful explanations in chain-of-thought prompting](https://arxiv.org/abs/2305.04388). *NeurIPS 2023*.
- Wang, X. et al. (2022). [Self-consistency improves chain of thought reasoning in language models](https://arxiv.org/abs/2203.11171). arXiv:2203.11171; *ICLR 2023*.
- Wason, P. C. (1966). Reasoning. In B. M. Foss (ed.), *New Horizons in Psychology*, 135–151. Penguin.
- Wei, A. (2025). Announcement of gold-medal-level performance by an OpenAI experimental reasoning model at IMO 2025. X (formerly Twitter), 19 July 2025.
- Wei, J. et al. (2022). [Chain-of-thought prompting elicits reasoning in large language models](https://arxiv.org/abs/2201.11903). *NeurIPS 2022*.
- Yao, S. et al. (2022). [ReAct: Synergizing reasoning and acting in language models](https://arxiv.org/abs/2210.03629). arXiv:2210.03629; *ICLR 2023*.
- Yao, S. et al. (2023). [Tree of Thoughts: Deliberate problem solving with large language models](https://arxiv.org/abs/2305.10601). *NeurIPS 2023*.
