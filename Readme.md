# T5 Text-to-SQL Model

A fine-tuned **T5** model that converts natural language questions into SQL queries.  
Example:  
_"Show me all employees older than 30"_ →  
`SELECT name FROM employees WHERE age > 30`

---

## 📊 Performance
- **Overall Accuracy:** ~65–75%  
- **Simple Queries** (single table): ~85–95%  
- **Medium Complexity** (2–3 table joins): ~65–75%  
- **Complex Queries** (nested subqueries): ~50–60%  
- **Syntax Correctness:** ~95%+

---

## 📌 Training Summary
- **Base Model:** T5  
- **Epochs:** 3  
- **Final Training Loss:** ~0.2833  
- **Validation Loss:** 0.39–0.43 range  
- **Training Time:** ~7h 54m

---

## 🚀 Usage
```python
from transformers import AutoTokenizer, AutoModelForSeq2SeqLM

model_path = "model"
tokenizer = AutoTokenizer.from_pretrained(model_path)
model = AutoModelForSeq2SeqLM.from_pretrained(model_path)

question = "List the names of all employees older than 30."
inputs = tokenizer(question, return_tensors="pt")
outputs = model.generate(**inputs, max_length=128)
print(tokenizer.decode(outputs[0], skip_special_tokens=True))
