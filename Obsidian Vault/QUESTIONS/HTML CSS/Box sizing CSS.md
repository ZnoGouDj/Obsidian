это свойство определяет вычисление общей ширины и высоты элемента.

По умолчанию ширина и высота элемента задается только для контента. ТО ЕСТЬ, если у нас 4 блока с width: 25%, и у какого нибудь появляется отступ/граница - то они не поместятся на одной строке. 

Для исправления этого поведения используют **box-sizing**:

1) content-box (default) - размер элемента + отступы = новый размер (контент расширяется)
2) border-box - размер элемента + отступы = тот же размер (контент сжимается внутрь) 

Считаются только внутрениие отступы (padding) и граница (border). 
Внешний отступ (margin) двигает бокс от внешних элементов.
Проще работать с border-box. 

![[box-sizingCSS.png]]