# ⚛️ React Hooks — Top 10 (excluyendo useState y useEffect)

Referencia rápida de los hooks más utilizados en proyectos frontend con React, ordenados por frecuencia de uso.

---

## 🚀 Rendimiento

### 1. `useCallback`
Memoriza una función para que no se recree en cada render. Útil cuando se pasa como prop a componentes hijos.

```jsx
const handleClick = useCallback(() => {
  doSomething(id);
}, [id]);
```

---

### 2. `useMemo`
Memoriza el resultado de un cálculo costoso. Solo recalcula si cambian sus dependencias.

```jsx
const sortedList = useMemo(() => {
  return items.sort((a, b) => a.name.localeCompare(b.name));
}, [items]);
```

---

### 8. `useTransition`
Marca actualizaciones de estado como no urgentes, permitiendo que la UI siga respondiendo mientras se procesan.

```jsx
const [isPending, startTransition] = useTransition();

startTransition(() => {
  setSearchQuery(input);
});
```

---

### 9. `useDeferredValue`
Difiere la actualización de un valor para priorizar renders más urgentes, similar a un debounce nativo de React.

```jsx
const deferredQuery = useDeferredValue(searchQuery);
```

---

## 🔵 Referencias

### 3. `useRef`
Guarda un valor mutable que persiste entre renders sin provocar re-render. Típico para acceder a elementos del DOM.

```jsx
const inputRef = useRef(null);

useEffect(() => {
  inputRef.current.focus();
}, []);
```

---

### 7. `useId`
Genera IDs únicos y estables para asociar elementos accesibles (labels, inputs) en SSR y CSR sin colisiones.

```jsx
const id = useId();

return (
  <>
    <label htmlFor={id}>Nombre</label>
    <input id={id} type="text" />
  </>
);
```

---

### 10. `useImperativeHandle`
Personaliza el valor expuesto por una ref a componentes padres, usado junto a `forwardRef` para APIs imperativas.

```jsx
useImperativeHandle(ref, () => ({
  focus: () => inputRef.current.focus(),
}));
```

---

## 🟣 Contexto

### 4. `useContext`
Consume un valor de un contexto de React sin necesidad de prop drilling a través de componentes intermedios.

```jsx
const theme = useContext(ThemeContext);
```

---

## 🟡 Estado

### 5. `useReducer`
Alternativa a `useState` para estado complejo. Maneja lógica de actualización mediante un reducer centralizado.

```jsx
const [state, dispatch] = useReducer(reducer, initialState);

dispatch({ type: 'INCREMENT' });
```

---

## 🟢 Sincrónico

### 6. `useLayoutEffect`
Como `useEffect`, pero se ejecuta sincrónicamente después de mutaciones del DOM y antes de que el navegador pinte.

```jsx
useLayoutEffect(() => {
  const { height } = ref.current.getBoundingClientRect();
  setHeight(height);
}, []);
```

---

## 📊 Resumen

| # | Hook | Categoría | Uso principal |
|---|------|-----------|---------------|
| 1 | `useCallback` | Rendimiento | Memorizar funciones |
| 2 | `useMemo` | Rendimiento | Memorizar cálculos |
| 3 | `useRef` | Referencia | Acceder al DOM / valores mutables |
| 4 | `useContext` | Contexto | Consumir contexto global |
| 5 | `useReducer` | Estado | Estado complejo con reducer |
| 6 | `useLayoutEffect` | Sincrónico | Leer el DOM antes del pintado |
| 7 | `useId` | Referencia | IDs únicos para accesibilidad |
| 8 | `useTransition` | Rendimiento | Actualizaciones no urgentes |
| 9 | `useDeferredValue` | Rendimiento | Diferir valores para renders pesados |
| 10 | `useImperativeHandle` | Referencia | Exponer API imperativa con ref |

---

> **Nota:** `useTransition` y `useDeferredValue` requieren **React 18+**. Los demás están disponibles desde React 16.8.
