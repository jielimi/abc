# 实例所用Scheam

以下element相关操作均需要使用该片段Schema，其中以用户自定义字段_**initProperty,city,name**_为例。

```markdown
使用Schema数据部分实例：
  <ECEntityClass typeName="TestPhysicalObject" >
    <BaseClass>bis:PhysicalElement</BaseClass>
    <ECNavigationProperty propertyName="relatedElement" relationshipName="TestPhysicalObjectRelatedToTestPhysicalObject" direction="Forward" readOnly="True"/>
    <ECProperty propertyName="longProp" typeName="long" displayLabel="an int64_t value" />
    <ECProperty propertyName="intProperty" typeName="int" displayLabel="an int32 value" />
    <ECProperty propertyName="city" typeName="string" displayLabel="an int32 value" />
    <ECProperty propertyName="name" typeName="string" displayLabel="an int32 value" />
  </ECEntityClass>
```

---

# 创建Element

用户自定义元素属性接口,其中用户自定义字段_**initProperty，ciyt，name**_与上述Scheam中字段相对应:

```
interface CustomProp extends GeometricElementProps {
  city: string;
  name: string;
  intProperty: number;
  placement: {
    origin: Point3d;
    angles: YawPitchRollAngles;
  };
}
```

```



```





