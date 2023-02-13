```js
import React, { useState } from "react";

const RadioForm = () => {
  const [selectedOption, setSelectedOption] = useState("");

  const handleOptionChange = (event) => {
    setSelectedOption(event.target.value);
  };

  const handleFormSubmit = (event) => {
    event.preventDefault();
    console.log(selectedOption);
  };

  return (
    <form onSubmit={handleFormSubmit}>
      <div>
        <input
          type="radio"
          value="option1"
          checked={selectedOption === "option1"}
          onChange={handleOptionChange}
        />
        Option 1
      </div>
      <div>
        <input
          type="radio"
          value="option2"
          checked={selectedOption === "option2"}
          onChange={handleOptionChange}
        />
        Option 2
      </div>
      <div>
        <input
          type="radio"
          value="option3"
          checked={selectedOption === "option3"}
          onChange={handleOptionChange}
        />
        Option 3
      </div>
      <button type="submit">Submit</button>
    </form>
  );
};

export default RadioForm;
```
