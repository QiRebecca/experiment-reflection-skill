# Experiment Reflection

A reusable Codex skill for turning completed experiments into explanations, credible improvements, and evidence about a research idea.

It classifies positive, negative, and unclear signals; audits implementation, data, measurement, design, and mechanism; and connects each diagnosis to a specific repair, reanalysis, or next experiment. Positive results receive the same scrutiny so their underlying mechanism and contribution can be explained in a paper.

The objective is to develop strong, credible support for the original research line. Every result returns to that claim, with explicit limits and a maintained record of what changed. The skill includes a [reflection template](references/reflection-template.md) for result inventories, diagnosis, next steps, and evidence synthesis.

## Install and use

```bash
git clone https://github.com/QiRebecca/experiment-reflection-skill.git ~/.codex/skills/experiment-reflection
```

Invoke `$experiment-reflection` with the research idea, experiment plan, results, and available logs or artifacts. For example:

> Use $experiment-reflection to interpret these completed experiments against our original claim. Diagnose why the results occurred, identify justified improvements, and update our research dossier.

It works independently and complements [Research Idea Audit](https://github.com/QiRebecca/research-idea-audit-skill), which develops and reviews the idea before experimentation. Reports follow the user's language unless requested otherwise.

## License

MIT. See [LICENSE](LICENSE).
