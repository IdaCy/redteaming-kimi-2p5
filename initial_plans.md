# redteaming Kimi 2.5

## general notes

main thing: evaluating against sabotage, also against other model (e.g., definitely opus 4.5)

## on the controlarena
https://github.com/UKGovernmentBEIS/control-arena

| Setting             | Description                                                         | Setup        | Timing | Scorers     |
|---------------------|---------------------------------------------------------------------|--------------|--------|-------------|
| AgentDojo           | Environment for evaluating robustness against prompt injection      | Simple       | Sync   | Programmatic|
| Apps                | Application development programming tasks                           | Simple       | Async  | Programmatic|
| Bash                | Bash tasks from the CTRL-Z paper (based on Stack Overflow)          | Simple       | Sync   | Programmatic|
| BashArena           | Successor to the BashBench dataset                                  | Simple       | Sync   | Programmatic|
| BigCodeBench        | Code generation benchmark with compositional reasoning tasks        | Simple       | Async  | Programmatic|
| Data Poisoning      | Distillation of a model (with collusion propensity side tasks)      | Simple       | Async  | LLM         |
| Eval Sabotage       | Dangerous capability evaluation codebase                            | Private repo | Async  | LLM         |
| IAC                 | Infrastructure codebase for root AWS account at mock frontier lab   | Simple       | Async  | Programmatic|
| Infra               | Training cluster kubernetes codebase                                | Complex      | Async  | Programmatic|
| Rogue Eval          | Inference logging toy setting                                       | Simple       | Async  | Programmatic|
| SAE Interp Sabotage | Sparse Autoencoder feature labelling                                | Simple       | Sync   | LLM         |
| SHADE Arena         | Real-world agent tasks such as bank transfers                       | Private repo | Sync   | LLM         |
| vLLM                | High-throughput LLM inference codebase                              | Simple       | Mixed  | Mixed       |

## discussed

Ram does:
- SHADE arena
- BashArena

I do:
1. rogue eval
2. data poisoning
considering some iac

we use:
- main model kimi 2.5; comparing against gemini 3 pro, gpt 5.2, opus 4.5
- monitor: gpt-5 nano
- we always track: side task success, main task success, detection
- we then analyse calculating evasion success rate
- we start with 1 run for testing, then add 2 more to check against, and check variance; if it's quite high we run more
- decisions based much on https://www.anthropic.com/research/shade-arena-sabotage-monitoring

## policies & protocols
- default attack and honest policies
- default trusted monitor protocol

# plans

**context:**
- working area for a technical AI Safety hackathon project on **red-teaming Kimi 2.5**
- listed possible tracks; we are choosing **Option 4: “propensity to blue-team / red-team (Shade Arena)”**

## the options were (for context, paraphrased):
1. agent jailbreaks / self-replication themes  
2. eval inspection / integration tooling  
3. coding-agent capability w/ many agents  
4. **propensity to blue-team vs red-team (e.g. Shade Arena)** (picked)  
5. values/alignment stress tests across framing/culture  
6. viral benchmarks as early risk indicators  
7. real-world failure modes (how people would actually use/misuse)  
8. model-internal deletion/obfuscation ideas  
9. fine-tuning effects

## 1) overview (what’s clear so far)

### trying to achieve
this is **not** a “benchmark Kimi’s intelligence” event - it’s a **technical AI safety** exercise

**goal:** produce **actionable evidence** about Kimi 2.5’s *safety-relevant behavior* under realistic pressure, especially:
- multi-turn conversations (not one-shot Q&A),
- ambiguous user intent (not cartoonishly malicious),
- gradual escalation and social engineering,
- “agent-like” framing where the model is embedded in a workflow

### plan emphasized “agentic evals vs QA evals”
the plan contrasted:
- **QA evals**: “ask question → grade answer”
- **agentic / behavioral evals**: “give situation → observe decisions over time”

### what “red-teaming Kimi 2.5” means here
- systematically probing **failure modes** and **misuse pathways**
- generating a **repeatable evaluation suite**
- comparing behavior across models or settings (optional but valuable)
but
- does **not** mean generating real-world harmful instructions, targeting real systems, or producing anything that increases operational misuse
- instead, keep scenarios **abstracted, fictionalized, and non-actionable**, focusing on decision boundaries and safety posture

this is *not* “can the model do dangerous things?”
it’s closer to:
> given ambiguous or manipulative framing, how quickly and how far does the model drift into unsafe assistance?


