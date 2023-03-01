```tsx
import React, { useState } from "react";
import { useForm } from "react-hook-form";

type FormValuesPage1 = {
  question1: string;
  question2: string;
};

type FormValuesPage2 = {
  question3: string;
  question4: string;
};

type FormData = FormValuesPage1 & FormValuesPage2;

type PropsPage1 = {
  register: ReturnType<typeof useForm>["register"];
  handleSubmit: ReturnType<typeof useForm>["handleSubmit"];
};

type PropsPage2 = {
  register: ReturnType<typeof useForm>["register"];
  handleSubmit: ReturnType<typeof useForm>["handleSubmit"];
};

const FormPage1 = ({ register, handleSubmit }: PropsPage1) => {
  return (
    <form onSubmit={handleSubmit}>
      <h2>Page 1</h2>
      <label>
        Question 1 :
        <input type="text" {...register("question1")} />
      </label>
      <br />
      <label>
        Question 2 :
        <input type="text" {...register("question2")} />
      </label>
      <br />
      <button type="submit">Next</button>
    </form>
  );
};

const FormPage2 = ({ register, handleSubmit }: PropsPage2) => {
  return (
    <form onSubmit={handleSubmit}>
      <h2>Page 2</h2>
      <label>
        Question 3 :
        <input type="text" {...register("question3")} />
      </label>
      <br />
      <label>
        Question 4 :
        <input type="text" {...register("question4")} />
      </label>
      <br />
      <button type="submit">Submit</button>
    </form>
  );
};

const MultiStepForm = () => {
  const [step, setStep] = useState(1);
  const {
    register,
    handleSubmit,
    formState: { errors },
  } = useForm<FormValuesPage1 | FormValuesPage2>();
  const [formData, setFormData] = useState<FormData>({});

  const onSubmitPage1 = (data: FormValuesPage1) => {
    setFormData({ ...formData, ...data });
    setStep(2);
  };

  const onSubmitPage2 = (data: FormValuesPage2) => {
    setFormData({ ...formData, ...data });
    // Submit the form to the backend
    console.log(formData);
  };

  return (
    <>
      {step === 1 && (
        <FormPage1 register={register} handleSubmit={handleSubmit(onSubmitPage1)} />
      )}
      {step === 2 && (
        <FormPage2 register={register} handleSubmit={handleSubmit(onSubmitPage2)} />
      )}
    </>
  );
};

export default MultiStepForm;

```

barre de progression
```tsx
import { useState } from "react";
import { useForm } from "react-hook-form";
import { Progress } from "tailwindcss-styled-components";

function MyForm() {
  const { register, handleSubmit, watch, formState } = useForm();
  const [currentPage, setCurrentPage] = useState(1);

  const onSubmit = (data: any) => {
    console.log(data);
    if (currentPage < 3) {
      setCurrentPage(currentPage + 1);
    } else {
      // submit to backend
    }
  };

  const progressValue = (currentPage / 3) * 100;

  return (
    <div>
      <Progress
        value={progressValue}
        className="h-4 bg-gray-300 rounded-full"
      >
        <div className="w-full h-full text-center text-xs text-white bg-blue-600 rounded-full">
          {progressValue}%
        </div>
      </Progress>
      {currentPage === 1 && (
        <div>
          <form onSubmit={handleSubmit(onSubmit)}>
            <label htmlFor="name">Name:</label>
            <input
              id="name"
              type="text"
              {...register("name", { required: true })}
            />
            {formState.errors.name && <span>This field is required</span>}
            <button type="submit">Next</button>
          </form>
        </div>
      )}
      {currentPage === 2 && (
        <div>
          <form onSubmit={handleSubmit(onSubmit)}>
            <label htmlFor="email">Email:</label>
            <input
              id="email"
              type="email"
              {...register("email", { required: true })}
            />
            {formState.errors.email && <span>This field is required</span>}
            <button type="submit">Next</button>
          </form>
        </div>
      )}
      {currentPage === 3 && (
        <div>
          <form onSubmit={handleSubmit(onSubmit)}>
            <label htmlFor="phone">Phone:</label>
            <input
              id="phone"
              type="tel"
              {...register("phone", { required: true })}
            />
            {formState.errors.phone && <span>This field is required</span>}
            <button type="submit">Submit</button>
          </form>
        </div>
      )}
    </div>
  );
}

```

```sql
-- Création de Table "users"

CREATE TABLE IF NOT EXISTS users (
	id SERIAL PRIMARY KEY,
	username VARCHAR(50),
	password VARCHAR(50),
	email VARCHAR(50),
	registration_date DATE,
	last_connection DATE
);

SELECT * FROM users;
```
