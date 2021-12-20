React动态收集`input`标签数据的方法

在Vue中,可以通过`v-model`双向绑定来收集`input`标签中的数据,但在React中没有类似的方法

可以通过以下方法实现

```jsx
export default class Index extends Component {
    state = {
        data: ""
    }
	// 获取input标签中的数据的函数
	getInput = (e) => {
        this.setState({
            data: e.target.value
        })
    }
    render() {
        return (
            <div className='index'>
                <input 
                	value = {this.state.data}
                    onChange = {this.getInput.bind(this)}
                />
            </div>
        )
    }
}
```

