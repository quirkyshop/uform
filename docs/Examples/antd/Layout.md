# 布局

> 表单布局问题，为什么会存在表单布局问题？
>
> 主要还是因为数据的输入场景会随业务场景做结构上的优化
>
> 减少信息噪音，降低误操作概率，最大化提升表单输入效率，所以，表单布局是表单解决
> 方案中很重要的一部分

## Normal

#### Demo 示例

```jsx
import React from 'react'
import ReactDOM from 'react-dom'
import {
  SchemaForm,
  Field,
  FormButtonGroup,
  Submit,
  Reset,
  FormItemGrid,
  FormCard,
  FormPath,
  FormBlock,
  FormLayout,
  createFormActions
} from '@uform/antd'
import { Button } from 'antd'
import Printer from '@uform/printer'
import 'antd/dist/antd.css'
const App = () => (
  <Printer>
    <SchemaForm>
      <FormLayout labelCol={8} wrapperCol={6}>
        <Field name="aaa" type="string" title="字段1" />
        <Field name="bbb" type="number" title="字段2" />
        <Field name="ccc" type="date" title="字段3" />
      </FormLayout>
      <FormButtonGroup offset={8}>
        <Submit>提交</Submit>​ <Reset>重置</Reset>​
      </FormButtonGroup>
    </SchemaForm>
  </Printer>
)
ReactDOM.render(<App />, document.getElementById('root'))
```

## Inline

> 内联布局

#### Demo 示例

```jsx
import React from 'react'
import ReactDOM from 'react-dom'
import {
  SchemaForm,
  Field,
  FormButtonGroup,
  Submit,
  Reset,
  FormItemGrid,
  FormCard,
  FormPath,
  FormBlock,
  FormLayout,
  createFormActions
} from '@uform/antd'
import { Button } from 'antd'
import Printer from '@uform/printer'
import 'antd/dist/antd.css'

const App = () => (
  <Printer>
    <SchemaForm inline>
      <Field name="aaa" type="string" title="字段1" />
      <Field name="bbb" type="number" title="字段2" />
      <Field name="ccc" type="date" title="字段3" />​
      <FormButtonGroup>
        <Submit>提交</Submit>​ <Reset>重置</Reset>​
      </FormButtonGroup>
    </SchemaForm>
  </Printer>
)
ReactDOM.render(<App />, document.getElementById('root'))
```

## Sticky

> 操作按钮组吸底，主要用于长表单

#### Demo 示例

```jsx
import React from 'react'
import ReactDOM from 'react-dom'
import {
  SchemaForm,
  Field,
  FormButtonGroup,
  Submit,
  Reset,
  FormItemGrid,
  FormCard,
  FormPath,
  FormBlock,
  FormLayout,
  createFormActions
} from '@uform/antd'
import { Button } from 'antd'
import Printer from '@uform/printer'
import 'antd/dist/antd.css'

const App = () => (
  <Printer>
    <SchemaForm labelCol={8} wrapperCol={6}>
      <Field name="aaa" type="string" title="字段1" />
      <Field name="bbb" type="number" title="字段2" />
      <Field name="ccc" type="date" title="字段3" />​
      <FormButtonGroup sticky offset={8}>
        <Submit>提交</Submit>​ <Reset>重置</Reset>​
      </FormButtonGroup>
    </SchemaForm>
  </Printer>
)
ReactDOM.render(<App />, document.getElementById('root'))
```

## Nested

> 嵌套布局
>
> 1. 使用 FormLayout 实现局部控制
>    labelCol/wrapperCol/size/labelAlign/labelTextAlign
> 1. 使用 FormCard 实现卡片式分离表单模块
> 1. 使用 FormBlock 实现在卡片内部的区块化分割
> 1. 使用 FormItemGrid 实现表单字段的局部网格布局能力
> 1. 使用 FormTextBox 实现表单文本化串联

#### Demo 示例

```jsx
import React, { useState } from 'react'
import ReactDOM from 'react-dom'
import {
  SchemaForm,
  Field,
  FormButtonGroup,
  Submit,
  Reset,
  FormItemGrid,
  FormTextBox,
  FormCard,
  FormPath,
  FormBlock,
  FormLayout,
  createFormActions
} from '@uform/antd'
import { Button } from 'antd'
import Printer from '@uform/printer'
import 'antd/dist/antd.css'

const App = () => {
  const [state, setState] = useState({ editable: true })
  return (
    <Printer>
      <SchemaForm
        editable={state.editable}
        labelCol={8}
        wrapperCol={6}
        onSubmit={v => console.log(v)}
      >
        <FormCard title="基本信息">
          ​<Field name="aaa" type="string" title="字段1" />
          ​<Field name="bbb" type="number" title="字段2" />
          ​<Field name="ccc" type="date" title="字段3" />​
        </FormCard>
        ​<FormCard title="详细信息">
          <FormLayout labelCol={8} wrapperCol={12}>
            <FormItemGrid title="字段3" gutter={10} cols={[6, 11]}>
              ​<Field name="ddd" type="number" />
              ​<Field name="eee" type="date" />​
            </FormItemGrid>
            <Field type="object" name="mmm" title="对象字段">
              <FormItemGrid gutter={10} cols={[6, 11]}>
                ​<Field name="ddd1" default={123} type="number" />
                ​<Field name="[startDate,endDate]" type="daterange" />​
              </FormItemGrid>
            </Field>
          </FormLayout>
          <FormLayout labelCol={8} wrapperCol={16}>
            <FormTextBox title="文本串联" text="订%s元/票 退%s元/票 改%s元/票">
              <Field type="number" default={10} required name="aa1" />
              <Field type="number" default={20} required name="aa2" />
              <Field type="number" default={30} required name="aa3" />
            </FormTextBox>
          </FormLayout>
          <Field name="aas" type="string" title="字段4" />​
          <FormBlock title="区块">
            ​<Field name="ddd2" type="string" title="字段5" />​
            <Field name="eee2" type="string" title="字段6" />​
          </FormBlock>
        </FormCard>​
        <FormButtonGroup offset={8} sticky>
          ​ <Submit>提交</Submit>​
          <Button
            type="primary"
            onClick={() => setState({ editable: !state.editable })}
          >
            {state.editable ? '详情' : '编辑'}
          </Button>
          <Reset>重置</Reset>​
        </FormButtonGroup>
      </SchemaForm>
    </Printer>
  )
}
ReactDOM.render(<App />, document.getElementById('root'))
```

## Grid

> 网格布局，主要用于列表查询场景的筛选项表单布局方式同样，使用 FormItemGrid

#### Demo 示例

```jsx
import React from 'react'
import ReactDOM from 'react-dom'
import {
  SchemaForm,
  Field,
  FormButtonGroup,
  Submit,
  Reset,
  FormItemGrid,
  FormCard,
  FormPath,
  FormBlock,
  FormLayout,
  FormTextBox,
  createFormActions
} from '@uform/antd'
import { Button } from 'antd'
import Printer from '@uform/printer'
import 'antd/dist/antd.css'

const App = () => (
  <Printer>
    <SchemaForm onSubmit={v => console.log(v)}>
      <FormItemGrid gutter={20}>
        <Field type="string" name="a1" title="查询字段1" />
        <Field type="string" name="a2" title="查询字段2" />
        <Field type="string" name="a3" title="查询字段3" />
        <Field type="string" name="a4" title="查询字段4" />
      </FormItemGrid>
      <FormItemGrid gutter={20} cols={[6, 6]}>
        <Field type="string" name="a5" title="查询字段5" />
        <Field type="string" name="a6" title="查询字段6" />
      </FormItemGrid>
      <FormButtonGroup style={{ minWidth: 150 }}>
        ​<Submit>提交</Submit>​<Reset>重置</Reset>​
      </FormButtonGroup>
    </SchemaForm>
  </Printer>
)
ReactDOM.render(<App />, document.getElementById('root'))
```

## 分步表单

```jsx
import {
  SchemaForm,
  Field,
  FormButtonGroup,
  Submit,
  FormEffectHooks,
  createFormActions,
  FormGridRow,
  FormItemGrid,
  FormGridCol,
  FormPath,
  FormLayout,
  FormBlock,
  FormCard,
  FormTextBox,
  FormStep
} from '@uform/antd'
import { Button } from 'antd'
import 'antd/dist/antd.css'

const { onFormInit$ } = FormEffectHooks

const actions = createFormActions()

let cache = {}

export default () => (
  <SchemaForm
    onSubmit={values => {
      console.log('提交')
      console.log(values)
    }}
    actions={actions}
    labelCol={{ span: 8 }}
    wrapperCol={{ span: 6 }}
    validateFirst
    effects={({ setFieldState, getFormGraph }) => {
      onFormInit$().subscribe(() => {
        setFieldState('col1', state => {
          state.visible = false
        })
      })
    }}
  >
    <FormStep
      style={{ marginBottom: 20 }}
      dataSource={[
        { title: '基本信息', name: 'step-1' },
        { title: '财务信息', name: 'step-2' },
        { title: '条款信息', name: 'step-3' }
      ]}
    />
    <FormCard name="step-1" title="基本信息">
      <Field name="a1" required title="A1" type="string" />
    </FormCard>
    <FormCard name="step-2" title="财务信息">
      <Field name="a2" required title="A2" type="string" />
    </FormCard>
    <FormCard name="step-3" title="条款信息">
      <Field name="a3" required title="A3" type="string" />
    </FormCard>
    <FormButtonGroup>
      <Submit>提交</Submit>
      <Button onClick={() => actions.dispatch(FormStep.ON_FORM_STEP_PREVIOUS)}>
        上一步
      </Button>
      <Button onClick={() => actions.dispatch(FormStep.ON_FORM_STEP_NEXT)}>
        下一步
      </Button>
      <Button
        onClick={() => {
          cache = actions.getFormGraph()
        }}
      >
        存储当前状态
      </Button>
      <Button
        onClick={() => {
          actions.setFormGraph(cache)
        }}
      >
        回滚状态
      </Button>
    </FormButtonGroup>
  </SchemaForm>
)
```
