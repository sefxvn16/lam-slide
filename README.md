# lam-slide

**English** | [Tiếng Việt](README.vi.md)

A Claude skill that keeps presentation slides faithful to the source document, so important content does not get lost. The skill only handles content; it does not build slide files. Building the file is handed off to whichever slide-creation skill you already use.

> The skill instructions (`SKILL.md`) are currently written in Vietnamese.

## What it does

When turning a document into slides, an AI tends to summarize and decide what goes on the slides in a single pass, and whatever gets dropped never shows up for the user to notice. This skill splits the work into 5 steps, with two stop points for user review:

1. **Full outline** of the source document (not a summary). Stop so the user can check it against the source and mark must-keep points.
2. **Slide framework with an explicit map**: which outline points each slide covers, and which points have not been placed yet. Stop so the user can approve and decide what to keep or drop.
3. **Hand the approved framework to a slide-creation skill** under a hand-off contract: fixed slide count, source fidelity level, must-keep list; receive the slides back together with the text of each slide.
4. **Outline-to-outline comparison**: compare the content of the built slides with the original outline and report what matches, what was dropped, and what was dropped intentionally.
5. **Manual editing by the user.**

## Boundaries

- The skill does **not** build .pptx files or slides itself, and does not replace a slide-creation skill.
- It picks the slide-creation skill in this order: the skill the user names → the skill the platform selects by default among the user's installed skills → the platform's built-in slide skill (if any) → ask the user. If no skill is available, it hands over the slide framework as text for the user to build.
- It is not meant for free-form creative slides that have no source document.

## Folder structure

```
lam-slide/
  SKILL.md
README.md
README.vi.md
LICENSE.md
```

## Installation

### Claude apps (claude.ai, Claude desktop)

1. Download the repo and zip the `lam-slide` folder on its own into `lam-slide.zip` (the zip must contain the `lam-slide` folder at its top level).
2. Open Claude, go to **Customize → Skills**, click **+** → **Create skill** → **Upload a skill**, and choose `lam-slide.zip`. Menu names and locations may differ between app versions. Skills require code execution to be enabled.
3. Check that `lam-slide` appears in the list and is turned on.

### Claude Code

Copy the `lam-slide` folder into `~/.claude/skills/` (available in all projects) or into a project's `.claude/skills/`, then restart Claude Code.

You need a slide-creation skill (or the platform's built-in one) to run Step 3.

## Usage

The skill triggers when you provide a source document and ask for slides, or when you call it directly with `/lam-slide`. Calling it directly is recommended if you have several slide-related skills installed and want to be sure this workflow runs. Examples:

- "Turn this report into 12 slides for the meeting: …"
- "/lam-slide Make slides from the two attached documents, keep all figures verbatim."

## Limitations

- The workflow has not been empirically validated. The design rationale in SKILL.md is a hypothesis.
- Step 4 needs the text of each slide. If the slide-creation skill cannot return it and the environment cannot read the file, you will be asked to provide it.
- Step 4 looks for points dropped from the original outline; it is not designed to detect content that was added.

## Feedback

Please send feedback through the repo's **Issues**. To make it easier to act on, include:

- your request and the type of source document (with personal or confidential information removed);
- the slide-creation skill you used in Step 3;
- the result you expected and the result you got.

Feedback is especially welcome on: the skill triggering when it should not (or not triggering), mismatches in the Step 3 hand-off, Step 4 missing dropped points, and instructions that are hard to follow.

## License

Released under **CC BY-NC 4.0**: free for non-commercial use with attribution. For commercial use, please contact the author via **Issues**. See [LICENSE.md](LICENSE.md).
