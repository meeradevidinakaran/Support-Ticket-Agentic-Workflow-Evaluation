#  Evaluations and Optimization at Scale

In Enterprise level use cases we might have to evaluate the AI workflow against 500+ test cases, over customized(scenario specific) metrics and continuous monitoring over several weeks.

**Build** - Build E2E Flow. We cannot evaluate a pipeline that is not built E2E.
**Define Ground Truth** - A Golden Dataset - These are the true statements that will be compared against AI output. This will be a collaborative efforts from SMEs - EMs. This will be an iterative process and we keep adding as and when we discover an edge case. 
**Choosing Right Metrics** - Each use case requires different metrics. Prioritize based on the requirement. Example : A workflow that calculates financial stats - prioritizes accuracy at first. Whereas a critical application like a Patient health monitor - would prioritize of Safety and Latency. Always combine the evaluation types LLM-as-a-judge + Human annotations. Customize your metrics as per the Use case. In this SaaS support ticket scenario, we prioritize Faithfulness to ensure the agent doesn't invent solutions for vague tickets like 'nothing works, fix it'.
**Record Baseline Version** - We cannot improve unless we have not measured a workflow. Run and Record Configuration setup + Prompts + tools + models of the baseline version for ensuring future enhancements. 
**Experiment on Fix at a time** - While **Changing Prompts** - utilize Global Variables or Prompt nodes to keep track of the different prompts tried in the same workflow instead of replacing it at each node. This allows an easier **fallback** method if this fix/ optimization does not work as expected. Test this with same Golden Data set, against same metrics and compare to baseline.  
**Track Each Experiment** - At scale experiments calls for explicit documentation giving more visibility and control parameters during the CI Loop.
**Rely on multiple Iterations** - LLM outputs are non deterministic by nature and same input can give different output each time. In this case consistency is when average improvement over time is positive. Even the worst output is better than baseline. 
**Combine Fixes** - If changing prompt and modifying LLM  both gives increased average. Combine them to assess whether they work together to give even better output.
**Regression Test** - Re run Tests that worked in baseline to ensure optimization fixes didn't break the workflow that worked fine before.

Avoid evaluating only the happy path, skipping documentation of experiments, ship only after improved scores over 5-6 runs not after a single good score.
