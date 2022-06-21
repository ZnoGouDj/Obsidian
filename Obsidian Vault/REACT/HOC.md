**компонент высшего порядка — это функция, которая принимает компонент и возвращает новый компонент.** HOC является чистой функцией без побочных эффектов. 

Могут быть использованы в следующих случаях:
1.  Переиспользование кода
2.  Слой абстракции для state и взаимодействия с ним
3.  Управление props

```js
const PcDisplay = (props) => {
  return (<div>
  <h1>{props.title}</h1>
  <p id="price">£{props.price}</p>
  <ul>
    <li><label>CPU</label> <span>{props.cpu}</span></li>
    <li><label>RAM</label> <span>{props.ram}</span></li>
    <li><label>SSD</label> <span>{props.ssd}</span></li>
  </ul>
  </div>);
};

// Implement HOC -> returns a functions that wraps the passed in `PcDisplay` component
let withPriceModel = (AnotherPcDisplay, i_price=0) => {
  return function(props){
    return (<AnotherPcDisplay {...props} price={i_price + 50} />)
    }
}

// Build basic and pro model components using `withPriceModel`
let BasicModel = withPriceModel(PcDisplay);

let ProModel = withPriceModel(PcDisplay, 60);
```