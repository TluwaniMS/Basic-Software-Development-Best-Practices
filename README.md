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

`NB!` Avoid nested loops at all times, because they leave the code in a messy state and make it hard to maintain.

```
const schools = [
  {
    name: "Kgwadu Primary School",
    students: [
      {
        name: "Lerato",
        age: 12,
        gender: "Male",
        grade: 6,
        sports: ["Soccer", "Swimming", "Rugby"]
      },
      {
        name: "Morokolo",
        age: 10,
        gender: "Male",
        grade: 4,
        sports: ["Soccer", "Rugby"]
      },
      {
        name: "Lufuno",
        age: 13,
        gender: "Female",
        grade: 7,
        sports: ["Netball", "Swimming"]
      }
    ]
  },
  {
    name: "Mamotshana Primary School",
    students: [
      {
        name: "Refilwe",
        age: 9,
        gender: "Female",
        grade: 3,
        sports: ["Netball"]
      },
      {
        name: "Kgaogelo",
        age: 10,
        gender: "Female",
        grade: 4,
        sports: ["Netball", "Swimming"]
      },
      {
        name: "Mokgadi",
        age: 8,
        gender: "Female",
        grade: 2,
        sports: []
      }
    ]
  },
  {
    name: "Mosima Primary School",
    students: [
      {
        name: "Hloni",
        age: 9,
        gender: "Male",
        grade: 3,
        sports: ["Soccer", "Rugby"]
      },
      {
        name: "Themba",
        age: 11,
        gender: "Male",
        grade: 5,
        sports: ["Soccer"]
      },
      {
        name: "Tebogo",
        age: 12,
        gender: "Male",
        grade: 6,
        sports: ["Swimming", "Rugby"]
      }
    ]
  }
];
```

* Requirements:

Get all the male students from every school that participate in both rugby and soccer.

`Bad Practice`

```
const maleStudentsThatParticipateInBothSoccerAndRugby = [];

schools.forEach((school) => {
  school.students.forEach((student) => {
    if (
      student.sports.includes("Soccer") &&
      student.sports.includes("Rugby") &&
      student.gender === "Male"
    ) {
      maleStudentsThatParticipateInBothSoccerAndRugby.push(student);
    } else {
      // pass
    }
  });
});
```

`Best Practice`

```
const maleStudentsThatParticipateInBothSoccerAndRugby = [];

const extractStudentsByGenderAndRelevantSports = (
  students,
  gender,
  ...sports
) => {
  const studentsMatchingTheRequiredParameters = [];

  students.forEach((student) => {
    const studentMatchesTheRequiredGender = student.gender === gender;
    const totalSportsTheStudentParticipatesInThatMatchTheRequiredSports = student.sports.filter(
      (sport) => sports.includes(sport)
    ).length;
    const totalSportsThatTheStudentIsRequiredToParticipateIn = sports.length;

    const totalSportsTheUserParticipatesInMatchesTheTotalSportsRequired =
      totalSportsTheStudentParticipatesInThatMatchTheRequiredSports ===
      totalSportsThatTheStudentIsRequiredToParticipateIn;

    studentMatchesTheRequiredGender &&
    totalSportsTheUserParticipatesInMatchesTheTotalSportsRequired
      ? studentsMatchingTheRequiredParameters.push(student)
      : "";
  });

  return studentsMatchingTheRequiredParameters;
};

schools.forEach((school) => {
  const studentsThatMatchTheRequiredParameters = extractStudentsByGenderAndRelevantSports(
    school.students,
    "Male",
    "Soccer",
    "Rugby"
  );

  maleStudentsThatParticipateInBothSoccerAndRugby.push(
    ...studentsThatMatchTheRequiredParameters
  );
});

```

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

`Bad Practice`

```
const productsInCart = [
  { name: "Soap", price: 10.5 },
  { name: "Meat", price: 25.0 },
  { name: "Milk", price: 12.0 },
  { name: "Bread", price: 15.0 }
];

const calculateProductsPriceWithTax = (products, valueAddedTax) => {
  const productsTotalPriceExcludingTax = products.reduce(
    (previousTotal, currentProductPrice) => {
      return previousTotal + currentProductPrice.price;
    },
    0
  );

  const productsTotalIncludingTax =
    productsTotalPriceExcludingTax * (1 + valueAddedTax);

  return productsTotalIncludingTax;
};

const createMessageToAlertUserOfTotalCartCost = (products) => {
  const totalCartCost = products.reduce(
    (previousTotal, currentProductPrice) => {
      return previousTotal + currentProductPrice.price;
    },
    0
  );

  return `Your cart requires R${totalCartCost} to be cleared.`;
};
```

`Good Practice`

```
const productsInCart = [
  { name: "Soap", price: 10.5 },
  { name: "Meat", price: 25.0 },
  { name: "Milk", price: 12.0 },
  { name: "Bread", price: 15.0 }
];

const calculateProductsPrice = (products) => {
  const productsTotalPrice = products.reduce(
    (previousTotal, currentProductPrice) => {
      return previousTotal + currentProductPrice.price;
    },
    0
  );

  return productsTotalPrice;
};

const calculateProductsPriceWithTax = (products, valueAddedTax) => {
  const productsTotalPriceExcludingTax = calculateProductsPrice(products);

  const productsTotalIncludingTax =
    productsTotalPriceExcludingTax * (1 + valueAddedTax);

  return productsTotalIncludingTax;
};

const createMessageToAlertUserOfTotalCartCost = (products) => {
  const totalCartCost = calculateProductsPrice(products);

  return `Your cart requires R${totalCartCost} to be cleared.`;
};
```

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
