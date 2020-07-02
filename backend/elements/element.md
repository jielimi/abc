# element

一个BIS元素代表了现实世界种的一个实体，例如泵，梁，合同，公司，流程，要求，文件，人员等。

元素的属性在schema中定义，BIS中的每个元素都来自元素类。

### FederationGuid

每个BIS元素都有一个可选的128位全局唯一标识符，称为FederationGuid。通常，FederationGuid是由外部系统分配的，用于将元素与它们的外部含义联合起来。

UserLabel

每个BIS元素都有一个可选的UserLabel属性，以提供用户熟悉的别名。UserLabel可以在GUI中提供另一个“更友好”的名称。例如，CodeValue=“R-134”的房间可能有UserLabel=“The Big Kitchen”或UserLabel=“John’s Office”。UserLabel上没有唯一性约束。除了数据转换程序之外，UserLabel总是留给用户输入，而不是通过编程生成。

