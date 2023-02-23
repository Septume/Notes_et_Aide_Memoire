le component est sur la route `localhost:3000/Form`

```tsx
const navigate = useNavigate();

const handletNextPage = () => {
	navigate("Page1")
};
```
Dans ce cas la route **rajoute** Page 1 => `localhost:3000/Form/Page1`

```tsx
const navigate = useNavigate();

const handletNextPage = () => {
	navigate("/Page1")
};
```
Dans ce cas la route **remplace** Page 1 => `localhost:3000/Page1`

```tsx
const navigate = useNavigate();

const handletNextPage = () => {
	navigate("/Form/Page1")
};
```
Dans ce cas la route **va directement** Page 1 => `localhost:3000/Form/Page1`