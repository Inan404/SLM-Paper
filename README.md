# Works on Souza et al.’s SLM paper

I mainly tried to observe why deep seek r1 14B was underperforming in code generation tasks in spite of  being a reasoning model and having the same number of parameters as the best performing phi model. My hypothesis was that the paper’s generalistic approach for all models led to a lot of parsing errors on the output of the deepseek model as a huge margin of the outputs from deepseek were flagged as ‘Not a Valid Answer’ .  DeepSeek-R1 14B's underperformance (23.9% pass@3) versus PHI-4 14B (63.6%) stems primarily from output serialization failures, the 35.5% "Not Answered" rate indicates the pipeline cannot extract valid code from verbose reasoning traces. I took multiple attemps on solving this, effectively increasing deepseek’s accuracy by minimizaing the mismatches between the parser and the model’s output and introducing smaller agents under deepseek to make the whole task modular.

The measures I took:

 (1) **Enhanced Parsing**: Implement AST-aware code extraction with regex fallbacks to handle mixed reasoning-code outputs and reduce the 16.4% compilation error rate. Trial and error of prompts and tuning model temperature and hyperparameter. Properly distinguishing the reasoning block of the model and the output block.

(2) **Agentic Decomposition**: Chain DeepSeek-R1's reasoning with PHI-4's code generation via an intermediate state encoder, leveraging reasoning strengths while mitigating code generation instability (64.2% vs 77.5% semantic consistency). 

(3) **Exact Reproduction**: Validate failures are methodology-agnostic by replicating Souza et al.'s protocol on the same 280 Codeforces problems with identical prompts. 

(4) **Distilled Models(Proposed, Not Implemented)** : Train lightweight student models on DeepSeek/Phi-14B reasoning trajectories to reduce output bloat (82.2 tokens average) while preserving correctness. This will leas us to get the accuracy found by Souza et al with smaller models fitting the purpose of the paper.

(5) **Recursive Error Correction( Proposed , not Implemented still)** : Implement verdict-driven iterative refinement loops where Codeforces failure signals (TLE, Runtime Error, Wrong Answer) inform correction prompts across up to 5 iterations. 

These interventions treat DeepSeek's failures as systems-level challenges rather than fundamental reasoning deficits.
