## Session 4: AI Agents for Empirical Research

**Track:** 2 — AI for Research
**Date:** TBD
**Presenter:** TBD
**Length:** 30 minutes

### Session Overview

AI coding agents are becoming increasingly capable of handling substantial parts of the empirical research workflow. They can search for information, inspect unfamiliar codebases, write and debug code, organize files, document decisions, execute multi-step tasks, and iterate on research pipelines with relatively limited supervision.

For empirical researchers, this raises a question that is broader than whether a particular tool is useful:

> **How should we organize, delegate, and verify empirical research when AI agents can execute a meaningful share of the workflow?**

The goal of this session is not to provide a tutorial on Claude Code or any other specific coding agent. Instead, we will use several concrete examples to think about how AI agents may change the way empirical research is conducted.

The discussion will focus on three related issues:

1. how AI agents may change the production process of empirical research;
2. how research projects can be structured so that agents can understand and work with them effectively;
3. how researchers should verify work produced or assisted by AI agents.

A recurring theme throughout the session is that the main challenge may increasingly shift from **writing every line of code ourselves** to **designing tasks, specifying constraints, evaluating outputs, and constructing credible verification procedures**.

### Readings
- Scott Cunningham — [*Claude Code, Research, and Publishing*](https://causalinf.substack.com/p/claude-code-27-research-and-publishing)

### Example Repositories
- [`paper-temp`](https://github.com/SITONGRUC/paper-temp) — an example research repository structure designed to be legible to an AI agent
- [`311_adoption_analysis`](https://github.com/SITONGRUC/311_adoption_analysis) — a case study delegating a real empirical task to an AI agent

---

### 1. AI Agents and the Production of Research

The Cunningham post provides a useful starting point for thinking about what happens when the cost of producing empirical research falls substantially.

Coding agents can potentially reduce the time required for many activities that traditionally consume a large amount of researcher effort: implementing empirical specifications, cleaning data, debugging code, collecting information from external sources, producing tables and figures, writing documentation, and maintaining research repositories.

If these tasks become substantially cheaper, the bottleneck in empirical research may move elsewhere. For example, the scarce skills may increasingly become:

- identifying interesting and important research questions;
- translating conceptual ideas into well-defined empirical tasks;
- deciding what evidence is actually informative;
- recognizing when an analysis is wrong despite producing plausible-looking output;
- designing validation and robustness procedures;
- maintaining a coherent research design across many agent-generated intermediate steps;
- exercising judgment about what should and should not be delegated.

**Questions for discussion**
- Which parts of empirical research are likely to become much cheaper because of AI agents? Which parts are unlikely to become cheap?
- If implementing an empirical analysis becomes easier, does research design become more important?
- Does the comparative advantage of a researcher shift from execution toward judgment and verification?
- What happens to the value of traditional programming skills if agents become very good at producing code?
- Could lower execution costs change the types of research questions that become feasible?

> **If an AI agent can execute much of an empirical project, what remains uniquely valuable about the researcher?**

### 2. Making a Research Project Legible to an AI Agent

AI agents work much better when a research project has a clear internal structure.

Researchers often carry a large amount of implicit information in their heads — which dataset is authoritative, which script generates a particular table, which files are obsolete, which variables have already been validated, which assumptions should never be changed. A human collaborator can often recover this information through conversation. An AI agent cannot reliably do so unless much of that implicit knowledge is made explicit.

The [`paper-temp`](https://github.com/SITONGRUC/paper-temp) example repository illustrates one possible structure:

- `data_raw/` for original source data
- `data_clean/` for processed datasets
- `src/` for analysis code
- `results/` for generated tables, figures, and other outputs
- `paper/` for manuscript-related files
- `docs/` for project documentation
- `prompts/` for important instructions or reusable agent tasks
- `logs/` for records of execution and debugging

The specific folder names are less important than the underlying principle:

> **The state of the research project should be understandable from the repository itself rather than existing only in the researcher's memory.**

**Explicit research instructions** an agent benefits from include a statement of the research question and project scope, an analysis plan, a data dictionary, descriptions of major datasets, instructions about which files may or may not be modified, requirements for reproducibility, and rules governing empirical claims and generated outputs — for example, that empirical claims should be traceable to generated tables/figures/datasets, uncertainty should be flagged rather than silently resolved, tables should be generated from code rather than manually edited, substantial modifications should be planned before implementation, analysis steps should leave execution logs, and important results should be independently reproducible.

These rules are useful not only because they constrain the agent — they also force the researcher to articulate standards that are often otherwise implicit.

> **How much of the researcher's implicit knowledge should be externalized so that an AI agent can reliably work on the project?**

If agent-assisted research becomes common, good research infrastructure may increasingly involve designing projects that are simultaneously understandable to the researcher, understandable to collaborators, reproducible by another researcher, and interpretable by an AI agent. In that sense, repository design may become part of research design.

### 3. Case Study: Delegating an Empirical Task to an AI Agent

The [`311_adoption_analysis`](https://github.com/SITONGRUC/311_adoption_analysis) repository provides a concrete example of using an AI agent for a real research task.

The purpose of the example is not to argue that an agent can completely automate empirical research. Instead, it illustrates the importance of distinguishing between **task execution** and **research credibility**. An agent may be able to perform a large amount of work quickly — that does not automatically imply that the resulting research output should be trusted.

Suppose the task requires identifying information across many cities, extracting dates or institutional details, organizing the information into a dataset, and documenting the corresponding sources. An agent may be very effective at searching for candidate sources, extracting relevant information, organizing results, writing code to process the information, producing intermediate datasets, identifying inconsistencies, and generating documentation. But the central research problem remains:

> **How do we know that the final dataset is correct?**

This distinction becomes especially important because AI-generated errors are often not obvious — an incorrect answer may still be well formatted, internally consistent, and superficially plausible. The researcher therefore needs a workflow in which agent-generated work produces evidence that can itself be inspected and audited.

### 4. A Framework: Plan, Work, Verification

**Plan.** Before asking the agent to execute a complicated task, define what the task actually is: the research objective, the unit of observation, the expected output, acceptable and unacceptable data sources, coding/data conventions, how ambiguous cases should be handled, what information should be recorded, and what counts as successful completion. The quality of agent output often depends heavily on the quality of the task specification.

A vague request like "Find the adoption dates for these cities" may produce plausible output. A more carefully designed task might instead require a source for every observation, preservation of the original source text, classification of source quality, flags for conflicting information, a record of unresolved cases, and independent validation against a second source where possible. The second task produces not only an answer but also an **audit trail**.

**Work.** The agent can then perform much of the mechanical execution — searching, scraping, coding, data cleaning, file organization, debugging, documentation, generating tables and figures, checking consistency across files, identifying suspicious observations. The agent is treated as an execution system operating within an explicitly defined research environment. The researcher does not necessarily need to supervise every individual action, but the workflow should be designed so that the important intermediate outputs are observable.

**Verification.** This is the most important stage. The central question should not be "Did the agent finish the task?" It should be:

> **What evidence would convince us that the output is correct?**

Verification may involve checking a random sample of observations manually, independently reconstructing selected observations, comparing multiple data sources, requiring citations or source records for extracted information, checking internal consistency, examining unusual or influential observations, reproducing important results with an independent implementation, and explicitly separating verified, ambiguous, and unresolved cases.

Software completion and research validity are different things. A script can run without errors. A dataset can have the expected number of observations. A regression can produce a clean table. None of these facts guarantees that the underlying empirical result is correct.

### 5. What Should Be Delegated?

**Relatively easy to delegate:** repetitive coding, reformatting, writing boilerplate, searching large numbers of sources, generating documentation, reproducing standard specifications, checking whether files or variables are consistent, producing alternative implementations.

**Requires much greater researcher involvement:** defining the construct of interest, determining whether a proxy is valid, evaluating whether an identifying assumption is credible, deciding how ambiguous observations should be treated, interpreting contradictory evidence, deciding whether a result is economically meaningful, deciding which robustness tests actually address a concern.

The boundary between these categories may change rapidly as the technology improves — that boundary itself is therefore worth discussing.

### Discussion

> **Which parts of empirical research would you be comfortable delegating to an AI agent, and which parts would you never delegate without independent verification?**

Related questions:
- When is independent verification actually necessary? What forms of verification are credible?
- Should an AI-generated dataset be treated differently from a dataset collected by human research assistants?
- Can another AI agent serve as an independent verifier?
- How much should researchers disclose about agent involvement in data construction and analysis?
- Does agent-assisted research make reproducibility easier or harder?
- If the cost of empirical execution falls dramatically, what becomes the binding constraint on research quality?

### Notes / Slides
- TBD

### Preparation
1. Read the Cunningham post.
2. Briefly browse the `paper-temp` repository.
3. Briefly browse the `311_adoption_analysis` repository.

There is no need to run any code before the session. The goal is not to learn a particular AI coding tool — the goal is to discuss how the availability of capable AI agents may change the organization, execution, and verification of empirical research.

[← Back to home](../index.md)
