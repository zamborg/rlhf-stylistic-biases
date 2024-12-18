# RLHF Stylistic Biases Paper Outline / Brainstorm | Dec 17th 2024

Paper Outline / Rough Framing:

**What is a stylistic bias?** We want to see whether or not the `reward-models` overfit to particular styles of text (assertive writing, length, ...). Preference towards these *style* markers is considered bias. 

### Dec 18th Status / Preperation

Use `lexica` to tag labeled RLHF datasets (`rewardbench` in particular) to determine potential stylistic biases in the data. 

##### Potential Structures / Research Questions:

Some Research Questions:

- **RQ1** What styles of texts do reward models prefer? Are there particular styles that are overrepresented in training data / reward-model score?
- **RQ2** How do these stylistic biases propagate into the reward-models? *Deeper look into the training data*
- **RQ3** In RLHF datasets, for RM's that exhibit stylistic biases, what boolean choices are made that could affect downstream language models?
  - EG: RLHF dataset for LLM contains an example: `Assertive | Non-Assertive`. If the RM prefers Assertive text by-in-large, then the model will be steered towards assertiveness. 
  - Fundamentally, RMs are used more for non-labeled LLM generations, so a preference towards particular styles of text could be harmful.

Some Thoughts:

- **Domain** What particular domains do we want to focus on? We could limit ourselves to a specific subset of RLHF datasets, but because this is an exploration into stylistic biases, we could also just evaluate against a generic corpus of text.
  - To do so we can take a large set of texts that would be *similar* to the texts that the RM would be exposed to (in the process of aligning an LLM). We can tag each of these texts in a given corpus with a set of stylistic lexica (eg: assertive, long, ...) and bucket them into categories. These lexica values are also continuous allowing for further investigation if necessary. 
  - We can then score each of these texts using a RM and see if there is a correlation between the stylistic lexica and the RM score.
    - **SPIKE @ZUBIN** We can save compute constraints (largely temporal to be fair) by taking evaluated reward-models and computing stylistic-lexica scores for existing corpuses. Note that this would likely result in non-equivalent sets of data *between* reward-models.
- **Goal / Orientation** What is the goal of the reward model, what texts is it trying to score, and how was it trained?
  - We can run style-ablations (**SPIKE ZUBIN** need to figure out how to do this) on prompts and response texts, for reward models that support this, and see how the RM score changes.
  - When looking at un-prompted texts (things that are not necessarily RLHF data, but rather from our LLM-corpus-dataset) we can see how the RM score changes by inserting or manipulating prompts. 
  - We could even develop a method / lookup table for observing the particular preferences of given RMs and provide the community with a filter-able tool to *choose* ideal RMs
  - We can even segment RLHF training and evaluation data into particular style-slices for users to choose from. (consider: *what flavor is your reward model?*)


#### Potential Paper Outline:

1. **Introduction**
   - What is a stylistic bias?
   - Why is it important to investigate stylistic biases in reward models?
   - What are the goals of this paper?
2. **Related Work**
   - What work has been done in the area of stylistic biases in reward models?
   - What are the limitations of existing work?
3. **Methodology**
   - How do we determine what is a *style* of text?
   - What are our datasets? Curated? Human-Annotated? LLM-Generated? Prompted/Unprompted?
   - How do we compute *reward-scores* for our particular RMs?
   - **Pairwise Analysis?** **Style Ablations**? **Prompt Insertions**?
4. **Results**
5. **Discussion**

