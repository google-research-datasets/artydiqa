# ArTyDi-QA

**ArTyDi-QA** is a dataset for Modern Standard Arabic (MSA) designed for **Question Answering (QA)** and **Question Generation (QG)** tasks. It is derived from the Arabic subset of the TyDi QA benchmark and adapted into a SQuAD 2.0-style extractive format.

The dataset features natively authored, information-seeking questions and incorporates paragraph-level unanswerable questions.

## Structure

The dataset is organized into two compressed archives. All data is provided in standard **JSONL (JSON Lines)** format.

### `QA.zip`
Contains the Extractive QA dataset. This subset includes both **answerable** and **unanswerable** questions.
- `train.jsonl`
- `val.jsonl`
- `test.jsonl`

### `QG.zip`
Contains the Question Generation dataset. This subset consists strictly of **answerable** context-question pairs, ideal for training generative models.
- `train.jsonl`
- `val.jsonl`
- `test.jsonl`

## Data Format

Each line in the `.jsonl` files represents a single data example as a valid JSON object with the following fields:

| Field | Type | Description |
| :--- | :--- | :--- |
| `id` | String | A unique identifier for the example. |
| `title` | String | The title of the Wikipedia article from which the context was extracted. |
| `context` | String | The paragraph text providing the information context. |
| `question` | String | The question text relating to the context. |
| `answers` | Object | An object containing the ground truth answer(s). See structure below. |

### The `answers` Object

The `answers` field is a dictionary containing lists, allowing for multiple valid answers or spans:

- **`text`** (`List[String]`): A list of acceptable answer strings.
- **`start_char`** (`List[Int]`): A list of the starting character indices for the answer spans in the `context`.
- **`end_char`** (`List[Int]`): A list of the ending character indices for the answer spans in the `context`.

### Special Answer Types

**Unanswerable Questions**
In the **QA** subset, approximately 29% of the questions are unanswerable based on the provided paragraph. For these examples:
- **`text`**: Contains the string `"لا يمكن الإجابة على السؤال من النص"` (Cannot answer the question from the text).
- **`start_char`** and **`end_char`**: Set to `[-1]`.

**Yes/No Questions**
For binary questions where the answer is implicit in the text but not a specific span:
- **`text`**: Contains either `"نعم"` (Yes) or `"لا"` (No).
- **`start_char`** and **`end_char`**: Set to `[-1]`.

## Statistics

| Statistic | ArTyDi-QA | ArTyDi-QG |
| :--- | :---: | :---: |
| **Total Examples** | 24,120 | 17,183 |
| Train Examples | 18,272 | 12,962 |
| Validation Examples | 4,523 | 3,223 |
| Test Examples | 1,325 | 998 |
| Yes/No Questions | 6% | 8.5% |
| Unanswerable | 29% | N/A |
