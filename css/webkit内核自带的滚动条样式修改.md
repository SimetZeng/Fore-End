```css
::-webkit-scrollbar/*整体部分*/
{
  width: 10px;
  height:10px;
}

::-webkit-scrollbar-track/*滑动轨道*/
{
  -webkit-box-shadow: inset 0 0 5px rgba(0,0,0,0.2);
  border-radius: 0px;
  background: rgba(0,0,0,0.1);
}

::-webkit-scrollbar-thumb/*滑块*/
{
  border-radius: 5px;
  -webkit-box-shadow: inset 0 0 5px rgba(0,0,0,0.2);
  background: rgba(0,0,0,0.2);
}

::-webkit-scrollbar-thumb:hover/*滑块效果*/
{
  border-radius: 5px;
  -webkit-box-shadow: inset 0 0 5px rgba(0,0,0,0.2);
  background: rgba(0,0,0,0.4);
}
```
