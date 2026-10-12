# Words, for a plan written in English

<!-- Taken from the "Words" section of the upstream html-plan SKILL.md (Apache-2.0); see ../NOTICE. -->

Use this page when the plan is in English. For a Chinese plan, follow “中文写作” in SKILL.md.

The exhibits are the plan. Words only name them.

**Write all prose in ASD-STE100 Simplified Technical English (STE). Use no other style.** This rule applies to claims, captions, pins, questions, options and notes.

- **Approved words only.** Use a word only if the STE dictionary approves it, and only with its approved meaning and part of speech. If you are not sure about a word, use the most common short word that has the same meaning.
- **Technical names and technical verbs are permitted.** Names from the code (`createScheduled()`, `scheduled_messages`), product names, UI labels and units are technical names. Verbs of the field (*compile*, *deploy*, *merge*, *render*) are technical verbs. Use the same name for the same thing each time.
- **Short sentences.** One topic for each sentence. An instruction has 20 words at most. A description has 25 words at most. A paragraph has 6 sentences at most.
- **Active voice.** Say who does what: “The worker claims the row.” Not “The row is claimed.”
- **Simple tenses.** Use the present, the past and the future: *sends*, *sent*, *will send*. Do not write *has sent* or *is sending*. Do not use an *-ing* word unless it is part of a technical name.
- **Instructions are commands.** “Run the migration.” Write one instruction in each sentence. Put the condition first: “If the claim fails, stop.”
- **`must` and `can`.** Use *must* for a rule and *can* for what is possible. Do not use *should*, *may* or *might*.
- **Noun groups of 3 words at most.** “The retry limit of the send worker.” Not “the send worker retry limit setting”.
- **Full grammar.** Keep *the*, *a* and *an*. Do not use contractions, idioms, metaphors or jokes.

| Do not write | Write |
|---|---|
| utilize, leverage | use |
| perform, carry out | do |
| ensure, verify, check (as a verb) | make sure |
| demonstrate, indicate | show |
| commence, begin · terminate | start · stop |
| obtain · provide | get · give |
| prior to · in order to | before · to |
| however · additionally | but · also |
| about 50 | approximately 50 |

These are not STE and stay as they are: the words of the user in a `doc-quote`, code, and the text on a UI mockup.

- A caption is one sentence: what to notice. A pin is a clause. An option's `<small>` is 12 words at most.
- No paragraph between a claim and its exhibit. If the exhibit needs explaining, pick a better exhibit.
- The `h1` names the change and the place in 3 to 7 words: “Scheduling Sent Messages in PostBox”.

`pack.mjs` warns about some STE errors: common unapproved words, contractions, *has/have* tenses, the passive voice and long sentences. It does not know the full dictionary, so a clean run does not prove that the text is STE.
