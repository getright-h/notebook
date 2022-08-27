### 0.小点

1. `htmlfor` 给label添加htmlFor属性后，点击label时，Input框自动聚焦

   ```html
   <label htmlFor="insertArea">请输入内容</label>
   <input
      id="insertArea"
      className="input"
      value={this.state.inputValue}
      onChange={this.handleInputChange.bind(this)}
      />
   ```

   