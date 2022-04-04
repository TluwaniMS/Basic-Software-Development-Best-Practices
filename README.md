# Basic-Software-Development-Best-Practices

## 1. Function Rules:

Functions should either `answer` something or `do` something.

`Answer`
```
const user = {
  name: "Lerato",
  gender: "Female"
};

const checkIfUserIsAFemale = (user) => user.gender === "Female";
```

`Do`
```
const user = {
  name: "Lerato",
  gender: "Female"
};

const generateAnEmailForTheUser = (user) => `${user.name}@mock.com`;
```
## 2. Variable / Function Naming Best Practices:
## 3. Deep Nesting / Nested Loops:
## 4. Higher Order Array Functions Callback Function Parameters:
## 5. DRY (Don't Repeat Yourself:
