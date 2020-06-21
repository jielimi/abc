# 导入Schema

Schema片段：注意用户自定义新增字段: _**city,amount**_.在后续代码中将被使用。

```
  <ECEntityClass typeName="TestPhysicalElement">
        <BaseClass>bis:DefinitionElement</BaseClass>
        <ECProperty propertyName="testProperty" typeName="string"/>
	<ECProperty propertyName="city" typeName="string" displayLabel="this is a country" />
	<ECProperty propertyName="amount" typeName="int" displayLabel="this is an age" />
  </ECEntityClass>
```

---

# 测试代码

测试代码如下所示:

```js
import {
  SnapshotDb,
  BackendRequestContext,
  DefinitionModel,
} from "@bentley/imodeljs-backend";
import { DefinitionElementProps, IModel, Code } from "@bentley/imodeljs-common";
function createSnapshotFromSeed(
  testFileName: string,
  seedFileName: string
): SnapshotDb {
  const seedDb: SnapshotDb = SnapshotDb.openFile(seedFileName);
  const testDb: SnapshotDb = SnapshotDb.createFrom(seedDb, testFileName);
  seedDb.close();
  return testDb;
}
interface CustomProp extends DefinitionElementProps {
  city: string;
  amount: number;
}

class ElementTest {
  public constructor() {
    const seedBimFilePath = "D:\\iModel-Study\\1\\Seed.bim";
    const exampleBimFilePath = "D:\\iModel-Study\\1\\test.bim";

    this.imodelDb = createSnapshotFromSeed(seedBimFilePath, exampleBimFilePath);
    this.elementId = "";
  }
  private InsertElement() {
    const CustomElementProp = this.GetElementProp();
    this.elementId = this.imodelDb.elements.insertElement(CustomElementProp);
  }
  private GetElementProp() {
    const CustomElementProp: CustomProp = {
      classFullName: "TestBim:TestPhysicalElement",
      city: "北京",
      amount: 1500,
      model: DefinitionModel.insert(
        this.imodelDb,
        IModel.rootSubjectId,
        "example"
      ),
      code: Code.createEmpty(),
    };
    return CustomElementProp;
  }
  private async ImportExampleSchema() {
    const SchemaFilePath =
      "D:\\iModel-Study\\console-imodel\\TestBim.ecschema.xml";
    const requestContext = new BackendRequestContext();
    await this.imodelDb.importSchemas(requestContext, [SchemaFilePath]);
  }
  public CloseIModelDb() {
    //关闭打开的imodel数据文件对象
    if (this.imodelDb.isOpen) {
      this.imodelDb.close();
    }
  }
  public QueryElementProp() {
    //查询方式一
    const elementProp = this.imodelDb.elements.getElementProps<CustomProp>(
      this.elementId
    );
    if (elementProp) {
      console.log(elementProp.city); //输出    北京
      console.log(elementProp.amount); //输出  1500
    }
    //查询方式二
    const elementExProp = this.imodelDb.elements.getElementProps(
      this.elementId
    );
    if (elementExProp) {
      const jsongObject = JSON.parse(JSON.stringify(elementExProp));
      console.log(jsongObject.city); //输出    北京
      console.log(jsongObject.amount); //输出  1500
    }
  }
  public QueryElement() {
    const element = this.imodelDb.elements.getElement(this.elementId);
    if (element) {
      console.log(element.classFullName); //输出 TestBim:TestPhysicalElement
    }
  }
  //测试驱动函数入口
  public static Handle() {
    const elementTest = new ElementTest();
    //将测试Schema导入到imodel中;
    elementTest.ImportExampleSchema();
    //在imodel中新插入一个待测试Element.
    elementTest.InsertElement();
    //在imodel中查询指定的element的属性；
    elementTest.QueryElementProp();
    //在imodel中查询查询指定的element;
    elementTest.QueryElement();
    elementTest.CloseIModelDb();
  }

  private elementId: string; //新创建的element的ID
  private imodelDb: SnapshotDb; //打开的bim文件在内存中的对象;
}
export { ElementTest };

```



