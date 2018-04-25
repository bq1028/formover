# Formover

Formik x React Popper

## Why?

Forms that live in popovers like Airbnb's search filters.

## How

```
yarn add formik formover react-popper
```

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { FormikActions, Form, Field } from 'formik';
import { FormoverProps, PopoverProps, Formover } from 'formover';

const Button: React.SFC<any> = ({ innerRef, ...props }) => (
  <button ref={innerRef} {...props} />
);

export interface FormValues {
  email: string;
}
const App = () => (
  <div className="App">
    <h1 className="App-Title">Formik + React-Popper = Formover</h1>
    <Formover
      onSubmit={(
        values: FormValues, // form values
        formikActions: FormikActions<FormValues>, // formik bag
        popperActions: PopoverProps // close, toggle, isOpen
      ) => {
        setTimeout(() => {
          alert(JSON.stringify(values, null, 2));
          formikActions.setSubmitting(false);
          popperActions.close();
        }, 500);
      }}
      initialValues={{ email: '' }}
      target={({ getTargetProps }) => (
        <Button {...getTargetProps()}>Hello</Button>
      )}
    >
      {(props: FormoverProps<FormValues>) => (
        <Form>
          <Field name="email" autoFocus={true} placeholder="Email" />
          <button onClick={props.toggle}>Cancel</button>
          <button type="submit">Apply</button>
        </Form>
      )}
    </Formover>
  </div>
);
```

---

MIT License