# element

一个BIS元素代表了现实世界种的一个实体，例如泵，梁，合同，公司，流程，要求，文件，人员等。

元素的属性在schema中定义，BIS中的每个元素都来自元素类。

### FederationGuid

每个BIS元素都有一个可选的128位全局唯一标识符，称为FederationGuid。通常，FederationGuid是由外部系统分配的，用于将元素与它们的外部含义联合起来。

UserLabel

每个BIS元素都有一个可选的UserLabel属性，以提供用户熟悉的别名。UserLabel可以在GUI中提供另一个“更友好”的名称。例如，CodeValue=“R-134”的房间可能有UserLabel=“The Big Kitchen”或UserLabel=“John’s Office”。UserLabel上没有唯一性约束。除了数据转换程序之外，UserLabel总是留给用户输入，而不是通过编程生成。

JsonProperties

JsonProperties成员以JSON格式保存元素上特定于实例的临时数据。它是一个键-值对的字典，其中键是一个名称空间，值是一个JSON对象。通过这种方式，JsonProperties成员可以在任何元素上保存任何形式和复杂的外部定义（即在BIS之外）的数据。

为了避免命名值的冲突，JsonProperties成员的顶级名称被保留位名称空间。因此应该选择足够昌的唯一性名称空间，以避免冲突按照惯例（至少8个字符）。注意：所有JSON属性以及名称空间都是区分大小写的。

The UserProps namespace

JsonProperties有一个名为UserProps的保留名称空间。UserProps名称空间中的所有值都是用户添加的，应用程序代码不应该将信息存储在那里。用户应该使用自己的名称作用域规则将属性存储在名称中，比如大写前缀以避免冲突。但是，因为他们指定只有他们的数据保存在UserProps中，所以他们不需要担心与应用程序的冲突。

例如，一个元素可能有以下一组JsonProperties：

```js
{
  "SLYSOFT_props": {
    "partType": "st-10",
    "partName": "runner*144"
  },
  "IGASPEC_domFlow": {
    "max": 100,
    "min": 22
  },
  "UserProps": {
    "BTTE_vendorInfo": {
      "name": "Ace Manufacturing",
      "contractId": "1032SW3"
    },
    "BTTE_approvals": {
      "reviewers": ["Tom", "Justine", "Nate"],
      "date": "2018-02-11",
      "notes": ""
    }
  }
}
```

### JsonProperties的优点和缺点

JSON属性的最大优点是它们根本不需要任何schema或预先工作。

JSON属性的缺点是：

1. 没有类型安全，没有控制为任何属性名称存储什么内容的机制。
2. 没有必需的数据，对于要定义的某些属性，没有定义需求的机制。



