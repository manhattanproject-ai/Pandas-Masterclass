<div align="left">
  <h1> 7. Pandas Cheatsheet - Text Operations

  ## Text Operations

### 1. Build the sample Datasets : Data Generation

```py
import pandas as pd
import numpy as np
import random

# Seed for reproducibility
np.random.seed(42)
random.seed(42)

# --- Generate a large synthetic dataset ---
num_records = 10000 # Let's create 10,000 feedback entries

# Sample words for feedback
positive_words = ["excellent", "great", "awesome", "fantastic", "wonderful", "love", "satisfied"]
negative_words = ["bad", "poor", "terrible", "horrible", "disappointed", "slow", "buggy"]
neutral_words = ["ok", "average", "fine", "decent", "expected"]
product_words = ["service", "app", "website", "delivery", "product", "support", "feature"]

feedback_data = []

for i in range(num_records):
    user_id = f"user_{i+1:05d}"
    
    # Randomly choose sentiment for sentence construction
    sentiment_choice = random.choice(['positive', 'negative', 'neutral'])
    
    if sentiment_choice == 'positive':
        feedback_sentence = f"THE {random.choice(product_words).upper()} was {random.choice(positive_words).upper()}. VERY {random.choice(positive_words).upper()}!"
    elif sentiment_choice == 'negative':
        feedback_sentence = f"The {random.choice(product_words)} was {random.choice(negative_words)}. Very {random.choice(negative_words)}."
    else:
        feedback_sentence = f"The {random.choice(product_words)} was just {random.choice(neutral_words)}. nothing special."
        
    # Introduce random casing issues and leading/trailing spaces
    if random.random() < 0.3: # 30% chance of mixed case
        feedback_sentence = ''.join(random.choice([char.lower(), char.upper()]) for char in feedback_sentence)
    if random.random() < 0.2: # 20% chance of extra spaces
        feedback_sentence = "   " + feedback_sentence + "  "
    
    # Add some null values to simulate missing data
    if random.random() < 0.01: # 1% chance of null feedback
        feedback_sentence = np.nan

    feedback_data.append({
        'UserID': user_id,
        'FeedbackText': feedback_sentence,
        'Rating': random.randint(1, 5) # 1-5 star rating
    })

df = pd.DataFrame(feedback_data)

print(f"Original DataFrame head ({len(df)} records):")
print(df.head())
print("\nDataFrame Info (Note 'FeedbackText' dtype is 'object'):")
df.info()
print("-" * 30)
```
### 2. df.astype('string')
It adds the specified scalar value to every element within the DataFrame df.

```py
# Ensure the 'FeedbackText' column is of string type for .str accessor to work robustly
# Although often 'object' dtype works for strings, explicitly converting can be safer.
df['FeedbackText'] = df['FeedbackText'].astype('string')
print("\nAfter df['FeedbackText'].astype('string'):")
print(f"FeedbackText dtype: {df['FeedbackText'].dtype}")
print(df['FeedbackText'].head())
print("-" * 30)
```

### 3. df['column_name'].str.len()
It obtains the number of characters in the string values within columns.

```py
# Calculates the length of each string in the 'FeedbackText' column.
# Returns a Series of integers.
df['FeedbackLength'] = df['FeedbackText'].str.len()
print("\nAfter df['FeedbackText'].str.len():")
print(df[['FeedbackText', 'FeedbackLength']].head())
print(f"Average feedback length: {df['FeedbackLength'].mean():.2f}")
print("-" * 30)
```

### 4. Fill NaN values in 'FeedbackText'

```py
# Fill NaN values in 'FeedbackText' with an empty string temporarily for case conversions
# to avoid errors if a NaN is encountered, as .str methods propagate NaNs by default.
# We'll convert them back to None if needed, but for demonstration, we handle them.
df['CleanedFeedback'] = df['FeedbackText'].fillna('')
```

### 5. df['column_name'].str.lower()
It converts all strings in the column_name of the DataFrame df to lowercase.

```py
# Converts all characters in each string to lowercase.
df['FeedbackLower'] = df['CleanedFeedback'].str.lower()
print("\nAfter df['CleanedFeedback'].str.lower():")
print(df[['CleanedFeedback', 'FeedbackLower']].head())
print("-" * 30)
```

### 6. df['column_name'].str.upper()
It converts all strings in the column_name of the DataFrame df to uppercase.

```py
# Converts all characters in each string to uppercase.
df['FeedbackUpper'] = df['CleanedFeedback'].str.upper()
print("\nAfter df['CleanedFeedback'].str.upper():")
print(df[['CleanedFeedback', 'FeedbackUpper']].head())
print("-" * 30)
```
### 7. df['column_name'].str.title()
It returns a title-cased version of the string where every word starts with an uppercase character.

```py
# Converts the first character of each word to uppercase and the remaining to lowercase.
df['FeedbackTitle'] = df['CleanedFeedback'].str.title()
print("\nAfter df['CleanedFeedback'].str.title():")
print(df[['CleanedFeedback', 'FeedbackTitle']].head())
print("-" * 30)
```
### 8. df['column_name'].str.capitalize()
It returns only uppercases the first character of the entire string, regardless of the number of words present.

```py
# Converts the first character of the *entire string* to uppercase and the rest to lowercase.
df['FeedbackCapitalize'] = df['CleanedFeedback'].str.capitalize()
print("\nAfter df['CleanedFeedback'].str.capitalize():")
print(df[['CleanedFeedback', 'FeedbackCapitalize']].head())
print("-" * 30)
```
### 9. df['column_name'].str.swapcase()
It is used to convert every character in a string to a case that is opposite of its current one.

```py
# Swaps the case of each character in the string (uppercase becomes lowercase, and vice-versa).
df['FeedbackSwapcase'] = df['CleanedFeedback'].str.swapcase()
print("\nAfter df['CleanedFeedback'].str.swapcase():")
print(df[['CleanedFeedback', 'FeedbackSwapcase']].head())
print("-" * 30)
```
### 10. df['column_name'].str.casefold()
It is used to returns a case-folded copy of the string, which can be useful for caseless matching.

```py
# Converts strings to a case-folded form, which is more aggressive than .lower()
# for case-insensitive matching across different languages (e.g., 'ß' becomes 'ss').
df['FeedbackCasefold'] = df['CleanedFeedback'].str.casefold()
print("\nAfter df['CleanedFeedback'].str.casefold():")
print(df[['CleanedFeedback', 'FeedbackCasefold']].head())
print("-" * 30)
```
### Note
```py
# --- Important note: Handling NaN values ---
# All .str accessor methods (like .len(), .lower(), etc.) will return NaN for missing (NaN) values.
# If you want to perform operations and then fill NaNs or drop them, you'd do that separately.
# In our case conversions, we temporarily filled NaNs with '' to show the conversion;
# normally, you'd decide whether to drop NaNs or fill them appropriately before string ops.
```

### 11. Build the sample Datasets for String Check

```py
import pandas as pd
import numpy as np
import random
import string

# --- 1. Big Data Generation for String Checks ---
print("--- Generating Big Data for String Checks ---")

num_rows = 50000 # Let's create a large dataset with 50,000 rows
data = []

# Helper function to generate diverse string types
def generate_random_string(row_num):
    choice = random.randint(1, 10)
    
    if choice == 1: # Pure alphabetic
        return ''.join(random.choice(string.ascii_letters) for _ in range(random.randint(3, 10)))
    elif choice == 2: # Pure numeric (digits)
        return ''.join(random.choice(string.digits) for _ in range(random.randint(2, 7)))
    elif choice == 3: # Alphanumeric
        return ''.join(random.choice(string.ascii_letters + string.digits) for _ in range(random.randint(5, 12)))
    elif choice == 4: # Spaces
        return ' ' * random.randint(1, 5)
    elif choice == 5: # Lowercase
        return ''.join(random.choice(string.ascii_lowercase) for _ in range(random.randint(4, 9)))
    elif choice == 6: # Uppercase
        return ''.join(random.choice(string.ascii_uppercase) for _ in range(random.randint(4, 9)))
    elif choice == 7: # Title case (simple simulation)
        word = ''.join(random.choice(string.ascii_lowercase) for _ in range(random.randint(3, 7)))
        return word.capitalize()
    elif choice == 8: # Mixed case
        return ''.join(random.choice(string.ascii_letters) for _ in range(random.randint(5, 10)))
    elif choice == 9: # Contains decimal/numeric but not pure digit/numeric
        return str(random.randint(1, 100)) + '.' + str(random.randint(0, 9))
    else: # Empty or Mixed with special chars
        if random.random() < 0.2:
            return '' # Empty string
        else:
            return ''.join(random.choice(string.ascii_letters + string.digits + ' !@#$') for _ in range(random.randint(5, 15)))

for i in range(num_rows):
    data.append({'ID': i + 1, 'text_data': generate_random_string(i)})

df = pd.DataFrame(data)
print(f"Generated DataFrame with {num_rows} rows.")
print("Sample of generated data:")
print(df.head(10))
print("-" * 50)
```
### 12. df['column_name'].str.isalnum()
Checks whether all characters are alphanumeric in the column.

```py
# .str.isalnum(): Check if all characters in the string are alphanumeric (letters or numbers)
# Returns True if string has at least one character and all characters are alphanumeric, False otherwise.
df['is_alphanumeric'] = df['text_data'].str.isalnum()
print("\n'isalnum()' Check (first 50 True/False values):")
print(df['is_alphanumeric'].value_counts()) # Count True/False occurrences
```
### 13. df['column_name'].str.isalpha()
Checks whether all characters are alphabetic in the column.

```py
# Returns True if string has at least one character and all characters are alphabetic, False otherwise.
df['is_alphabetic'] = df['text_data'].str.isalpha()
print("\n'isalpha()' Check (first 50 True/False values):")
print(df['is_alphabetic'].value_counts())
```
### 14. df['column_name'].str.isdecimal()
Checks whether all characters are decimal in the column.

```py
# Returns True if string has at least one character and all characters are decimal, False otherwise.
# Differs from isdigit()/isnumeric() by excluding some Unicode characters like ² or ½.
df['is_decimal'] = df['text_data'].str.isdecimal()
print("\n'isdecimal()' Check (first 50 True/False values):")
print(df['is_decimal'].value_counts())
```
### 15. df['column_name'].str.isdigit()
Checks whether all characters are digits in the column.

```py
# Returns True if string has at least one character and all characters are digits, False otherwise.
# Includes some Unicode digits (e.g., Arabic numerals) but not decimals like '¾'.
df['is_digit'] = df['text_data'].str.isdigit()
print("\n'isdigit()' Check (first 50 True/False values):")
print(df['is_digit'].value_counts())
```
### 16. df['column_name'].str.islower()
Checks whether all characters are lowercase in the column.

```py
# Returns True if string has at least one cased character and all cased characters are lowercase, False otherwise.
df['is_lowercase'] = df['text_data'].str.islower()
print("\n'islower()' Check (first 50 True/False values):")
print(df['is_lowercase'].value_counts())
```
### 17. df['column_name'].str.isnumeric()
Checks whether all characters are numeric in the column.

```py
# Returns True if string has at least one character and all characters are numeric, False otherwise.
# Broadest category for numbers; includes digits, decimals, and even Roman numerals or fractions like '½'.
df['is_numeric'] = df['text_data'].str.isnumeric()
print("\n'isnumeric()' Check (first 50 True/False values):")
print(df['is_numeric'].value_counts())
```
### 18. df['column_name'].str.isspace()
Checks whether all characters are whitespace in the column.

```py
# Returns True if string has at least one character and all characters are whitespace, False otherwise.
df['is_whitespace'] = df['text_data'].str.isspace()
print("\n'is_whitespace()' Check (first 50 True/False values):")
print(df['is_whitespace'].value_counts())
```
### 19. df['column_name'].str.istitle()
Checks whether all characters are titlecase in the column.

```py
# Returns True if string has at least one cased character and is titlecased (first letter of each word capitalized, rest lowercase), False otherwise.
df['is_titlecase'] = df['text_data'].str.istitle()
print("\n'is_titlecase()' Check (first 50 True/False values):")
print(df['is_titlecase'].value_counts())
```
### 20. df['column_name'].str.isupper()
Checks whether all characters are uppercase in the column.

```py
# Returns True if string has at least one cased character and all cased characters are uppercase, False otherwise.
df['is_uppercase'] = df['text_data'].str.isupper()
print("\n'is_uppercase()' Check (first 50 True/False values):")
print(df['is_uppercase'].value_counts())
```










