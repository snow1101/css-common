```
import React, {useState} from 'react';
import { Button } from 'antd';
import './App.css';
import SortableTable from './SortableTable';
import SortableComponent from './SortableComponent';
import { PlusOutlined } from '@ant-design/icons';
import TestItem from './TestItem'
const initValue = [{name:'aaaa', des:"aaaaaaa", tag:[], fuTag:[]}, {name:'bbb', des:"aaaaaaa", tag:[], fuTag:[]}];
function App() {

  const [data, setData] = useState(initValue);
  const changeData = data => setData(data);
  const add = () => setData([...data,{name:'aaaa', des:"aaaaaaa", tag:[], fuTag:[]}])
  return (
    <div className="App">
      {/* <SortableTable dataSource={data} onChange={changeData} /> */}
      <SortableComponent data={data} onChange={changeData} renderItem={TestItem}/>
      <Button type="dashed" onClick={()=>add()} block icon={<PlusOutlined />}>
                Add field
              </Button>

    </div>
  );
}

export default App;




import React, { useState } from 'react';
import { sortableContainer, sortableElement, sortableHandle } from 'react-sortable-hoc';
import { MenuOutlined } from '@ant-design/icons';
import arrayMove from 'array-move';

export const DragIcon = sortableHandle(() => <MenuOutlined style={{ cursor: 'grab', color: '#999' }} />);
const SortableCompContainer = sortableContainer(({ children }) => <div>{children}</div>);

export const SortableItem = (WrappedComponent) => sortableElement(({ data }) => <WrappedComponent data={data} />);

function SortableComponent(props) {
    console.log(props);
    const {data, renderItem, onChange} = props;
    const SortItem = SortableItem(renderItem);
    const onSortEnd = ({ oldIndex, newIndex }) => onChange(arrayMove(data, oldIndex, newIndex));
    return (
        <SortableCompContainer onSortEnd={onSortEnd} disableAutoscroll useDragHandle>
            {data.map((item, i) =>
                <SortItem
                // don't forget to pass index prop with item index
                index={i}
                data={item}
                key={i}
                />
            )}
            </SortableCompContainer>
    )
}
export default SortableComponent;
                       
                       
                       
import React, {useState} from 'react';
import 'antd/dist/antd.css';
import { Table, Input, Button, Popconfirm, Form } from 'antd';
import { sortableContainer, sortableElement, sortableHandle } from 'react-sortable-hoc';
import { MenuOutlined } from '@ant-design/icons';
import arrayMove from 'array-move';

const DragHandle = sortableHandle(() => <MenuOutlined style={{ cursor: 'grab', color: '#999' }} />);
const handleDelete = () => {}
const columns = [
  {
    title: 'Name',
    dataIndex: 'name',
    render: () => (<Input value={1111} />)
  },
  {
    title: 'Sort',
    dataIndex: 'sort',
    width: 30,
    className: 'drag-visible',
    render: () => (
        <>
            <Popconfirm title="Sure to delete?" onConfirm={handleDelete}>
              <a>Delete</a>
            </Popconfirm>
            <DragHandle />
        </>
    ),
  },
];

const data = [
  {
    key: '1',
    name: 'John Brown',
    age: 32,
    index: 0,
  },
  {
    key: '2',
    name: 'Jim Green',
    age: 42,
    index: 1,
  },
  {
    key: '3',
    name: 'Joe Black',
    age: 32,
    index: 2,
  },
];

const SortableItem = sortableElement(props => <tr {...props} />);
const SortableContainer = sortableContainer(props => <tbody {...props} />);

// function SortableTable(props){
//     // const [dataSource, setDataSourse] = useState(data);
//  const {dataSource, onChange} = props;
// console.log(dataSource)
//   const onSortEnd = ({ oldIndex, newIndex }) => {
 
//     if (oldIndex !== newIndex) {
//       const newData = arrayMove([].concat(dataSource), oldIndex, newIndex).filter(el => !!el);
//       console.log('Sorted items: ', newData);
//       props.dataSource = newData;
//     //   setDataSourse(newData);
//         onChange(newData)
//     }
//   };

//   const DraggableContainer = props => (
//     <SortableContainer
//       useDragHandle
//       disableAutoscroll
//       helperClass="row-dragging"
//       onSortEnd={onSortEnd}
//       {...props}
//     />
//   );

//   const DraggableBodyRow = ({ className, style, ...restProps }) => {
//     console.log(dataSource)
//     // function findIndex base on Table rowKey props and should always be a right array index
//     const index = dataSource.findIndex(x => x.index === restProps['data-row-key']);
//     return <SortableItem index={index} key={index} {...restProps} />;
//   };



// return (
//     <Table
//     pagination={false}
//     dataSource={dataSource}
//     columns={columns}
//     rowKey="index"
//     components={{
//         body: {
//         wrapper: DraggableContainer,
//         row: DraggableBodyRow,
//         },
//     }}
//     />
// );
  
// }
// export default SortableTable;

class SortableTable extends React.Component {
  state = {
    dataSource: data,
  };

  onSortEnd = ({ oldIndex, newIndex }) => {
    const { dataSource } = this.state;
    if (oldIndex !== newIndex) {
      const newData = arrayMove([].concat(dataSource), oldIndex, newIndex).filter(el => !!el);
      console.log('Sorted items: ', newData);
      this.setState({ dataSource: newData });
    }
  };

  DraggableContainer = props => (
    <SortableContainer
      useDragHandle
      disableAutoscroll
      helperClass="row-dragging"
      onSortEnd={this.onSortEnd}
      {...props}
    />
  );

  DraggableBodyRow = ({ className, style, ...restProps }) => {
    const { dataSource } = this.state;
    // function findIndex base on Table rowKey props and should always be a right array index
    const index = dataSource.findIndex(x => x.index === restProps['data-row-key']);
    return <SortableItem index={index} {...restProps} />;
  };

  render() {
    const { dataSource } = this.state;

    return (
      <Table
      size="small"
        pagination={false}
        dataSource={dataSource}
        columns={columns}
        rowKey="index"
        components={{
          body: {
            wrapper: this.DraggableContainer,
            row: this.DraggableBodyRow,
          },
        }}
      />
    );
  }
}

export default SortableTable;




import React, { useEffect, useMemo, useState, memo } from 'react';
import SortableTable from './SortableTable';
import './index.css';
import { Row, Col, Form, Input} from 'antd';
import { DragIcon } from './SortableComponent';
const { TextArea } = Input;

function TestItem({data}) {
    console.log(data)
    const { name, des, tag, fuTag } = data;
    const [fields, setFields] = useState([{ name: ['username'], value: name }]);
    const [fold, setFold] = useState(false)
    
    const layout = {
        labelCol: { span: 8 },
        wrapperCol: { span: 16 },
      };
      const tailLayout = {
        wrapperCol: { offset: 8, span: 16 },
      };
    const showMore = () => {
        setFold(!fold)
    }
    const [form] = Form.useForm();
  return <div className={`test-item ${fold ? 'fold' : ''}`}>
      <Row>
        <Col span={18}>
        <Form
      {...layout}
      name="basic"
      fields={fields}
      form={form}
      onFieldsChange={(_, allFields) => {
        setFields(_)
        console.log(_)
        console.log(data)
      }}
  
    >
      <Form.Item
        label="Username"
        name="username"

        rules={[{ required: true, message: 'Please input your username!' }]}
      >
        <Input value={name} />
      </Form.Item>

      <Form.Item
        label="Password"
        name="password"
        rules={[{ required: true, message: 'Please input your password!' }]}
      >
        <TextArea />
      </Form.Item>
      <Form.Item
        label="tags"
        name="tags"
      >
        <SortableTable />
      </Form.Item>
    </Form>
        </Col>
        <Col span={6} > <a onClick={showMore}>{fold ? '展开' : '折叠'}</a><DragIcon /></Col>
    </Row>
    
  </div>;
}

export default memo(TestItem);

```
