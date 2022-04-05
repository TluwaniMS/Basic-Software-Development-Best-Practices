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

* Choose descriptive and clear names
* Use names according to their context

`Bad Practice`

```
const date =  new Date()
```

`Good Practice`

```
const currentDate = new Date()
```

`Bad Practice`

```
const getUser = (userId)=>{/*...*/}
```

`Good Practice`

```
const getUserById = (userId)=>{/*...*/}
```
## 3. Deep Nesting / Nested Loops:


## 4. Higher Order Array Functions Callback Function Parameters:

Avoid naming  `Higher Order Array Functions` `Callback Function` parameters with no context

`Bad Practice`

```
const numbers = [1, 2, 3, 4, 5];

const numbersMultipliedByTwo = numbers.map((resp) => resp * 2);
```

`Good Practice`

```
const numbers = [1, 2, 3, 4, 5];

const numbersMultipliedByTwo = numbers.map((number) => number * 2);
```
## 5. DRY (Don't Repeat Yourself:
## 6. Magic Numbers/Strings:

Avoid Magic strings/numbers at all costs, and rather create a file with enumerators or variables to contain the values.

`Bad Practice`

```
const totalWeeeksInAYear = 365 / 7;
```

`Good Practice`

```
const NUMBER_OF_DAYS_IN_A_WEEK = 7;

const NUMBER_OF_DAYS_IN_A_YEAR = 365;

const totalWeeksInAYear = NUMBER_OF_DAYS_IN_A_YEAR / NUMBER_OF_DAYS_IN_A_WEEK;
```
