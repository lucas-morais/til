# Gráfico de Linha com Recharts

- **Gráfico básico**
```jsx
import {
  Line,
  LineChart,
} from 'recharts';

const data = [
  {name:'valorX', value: 'valorY' } ...
];

function MeuGrafico() {

  <LineChart width={400} height={400} data={data}>
    <Line dataKey="value" stroke="#8884d8"/>
  </LineChart>
}
```

- **Adicionanedo elementos visuais**
```jsx
import {
  Line,
  LineChart,
   CartesianGrid, 
   XAxis, 
   YAxis

} from 'recharts';

const data = [
  {name:'valorX', value: 'valorY' } ...
];

function MeuGrafico() {

  <LineChart width={400} height={400} data={data}>
    <Line dataKey="value" stroke="#8884d8"/>
    <CartesianGrid />
    <XAxis dataKey="name">
    <YAxis>
  </LineChart>
}
```