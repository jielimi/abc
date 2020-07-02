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

