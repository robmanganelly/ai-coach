# AI Coach

A collection of skills for AI agents and chatbots focused on structured learning and progress tracking.

Each skill is a directory containing a `SKILL.md` file with instructions for the agent.

## Skills

* **tutor** — turns an LLM into a structured personal tutor using the Socratic method with a steering mechanism for when the student circles on a concept. Includes diagnostic placement, a skill map with levels 0-5, one question at a time, spaced review, and a final assessment. Adds short factual steering statements (1-2 sentences) when the student is stalled to avoid aporia while preserving discovery.
* **logger** — manages persistent session checkpoints for the tutor skill. Creates and updates session state files in a designated GitHub repository so tutoring progress can be resumed across sessions.

## How to use

With a coding agent that supports the common `SKILL.md` format, copy the skill directories into your agent's skills folder, then ask the agent to use them ("teach me X" for the tutor; the logger integrates with session start/end).

With a plain chatbot, paste the body of a skill's `SKILL.md` into the chat (or into a custom/system prompt), followed by what you want it to do.

Based on the structure of [janestreet/agent_skills](https://github.com/janestreet/agent_skills).