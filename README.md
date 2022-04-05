# Basic-Software-Development-Best-Practices

## 1. Function Rules:

i. Functions should either `Answer` something or `Do` something.

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

ii. Single Responsibility Principle.

`NB!` Functions should do only one thing .

`Bad Practice`

```
const generateAnArrayWithTenNumbersAnReturnTheEvenNumbers = () => {
  const arrayWithTenNumbers = [...Array(10).keys()];

  const evenNumbers = arrayWithTenNumbers.filter((number) => !(number % 2));

  return evenNumbers;
};
```

`Good Practice`

```
const arrayWithTenNumbers = [...Array(10).keys()];

const extractEvenNumbersFromArray = (numbersArray) => numbersArray.filter((number) => !(number % 2));
```

iii. Keep Thye Number Of Arguments As Low As Possible.

`Bad Practice`

```
const createNewUser = (name, surname, age, gender, height) => {/*...*/};

createNewUser("Thando", "Ndou", 28, "Male", 1.4);
```

`Good Practice`

```
const createNewUser = ({ name, surname, age, gender, height }) => {
  /*...*/
};

createNewUser({
  name: "Thando",
  surname: "Ndou",
  age: 28,
  gender: "Male",
  height: 1.4
});
```
## 2. Variable / Function Naming Best Practices:
## 3. Deep Nesting / Nested Loops:
## 4. Higher Order Array Functions Callback Function Parameters:
## 5. DRY (Don't Repeat Yourself:
