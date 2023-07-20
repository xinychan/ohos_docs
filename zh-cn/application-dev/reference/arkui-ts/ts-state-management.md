# 应用级变量的状态管理


状态管理模块提供了应用程序的数据存储能力、持久化数据管理能力、UIAbility数据存储能力和应用程序需要的环境状态。


>**说明：**
>
>本模块首批接口从API version 7开始支持，后续版本的新增接口，采用上角标单独标记接口的起始版本。


本文中T和S的含义如下：


| 类型   | 描述                                     |
| ---- | -------------------------------------- |
| T    | Class，number，boolean，string和这些类型的数组形式。 |
| S    | number，boolean，string。                 |


## AppStorage


### link<sup>10+</sup>

static link<T>(propName: string): SubscribedAbstractProperty<T>

与AppStorage中对应的propName建立双向数据绑定。如果给定的propName在AppStorage中存在，返回与AppStorage中propName对应属性的双向绑定数据。

双向绑定数据的修改会同步回AppStorage中，AppStorage会将变化同步到所有绑定该propName的数据和自定义组件中。

如果AppStorage中不存在propName，则返回undefined。


**参数：**

| 参数名      | 类型     | 必填   | 参数描述             |
| -------- | ------ | ---- | ---------------- |
| propName | string | 是    | AppStorage中的属性名。 |

**返回值：**

| 类型                                  | 描述                                       |
| ----------------------------------- | ---------------------------------------- |
| SubscribedAbstractProperty&lt;T&gt; | 返回双向绑定的数据，如果AppStorage不存在对应的propName，则返回undefined。 |


```ts
AppStorage.setOrCreate('PropA', 47);
let linkToPropA1 = AppStorage.link('PropA');
let linkToPropA2 = AppStorage.link('PropA'); // linkToPropA2.get() == 47
linkToPropA1.set(48); // 双向同步: linkToPropA1.get() == linkToPropA2.get() == 48
```


### setAndLink<sup>10+</sup>

static setAndLink&lt;T&gt;(propName: string, defaultValue: T): SubscribedAbstractProperty&lt;T&gt;

与Link接口类似，如果给定的propName在AppStorage中存在，则返回该propName对应的属性的双向绑定数据。如果不存在，则使用defaultValue在AppStorage创建和初始化propName，返回其双向绑定数据。

**参数：**

| 参数名          | 类型     | 必填   | 参数描述                                     |
| ------------ | ------ | ---- | ---------------------------------------- |
| propName     | string | 是    | AppStorage中的属性名。                         |
| defaultValue | T      | 是    | 当propName在AppStorage中不存在，使用defaultValue在AppStorage中初始化对应的propName。 |

**返回值：**

| 类型                                  | 描述                                       |
| ----------------------------------- | ---------------------------------------- |
| SubscribedAbstractProperty&lt;T&gt; | SubscribedAbstractProperty&lt;T&gt;的实例，和AppStorage中propName对应属性的双向绑定的数据。 |


```ts
AppStorage.setOrCreate('PropA', 47);
let link1: SubscribedAbstractProperty<number> = AppStorage.setAndLink('PropB', 49); // Create PropB 49
let link2: SubscribedAbstractProperty<number> = AppStorage.setAndLink('PropA', 50); // PropA exists, remains 47
```


### prop<sup>10+</sup>

static prop&lt;T&gt;(propName: string): SubscribedAbstractProperty&lt;T&gt;

与AppStorage中对应的propName建立单向属性绑定。如果给定的propName在AppStorage中存在，则返回与AppStorage中propName对应属性的单向绑定数据。如果AppStorage中不存在propName，则返回undefined。单向绑定数据的修改不会被同步回AppStorage中。

>**说明：**
> Prop仅支持简单类型。

**参数：**

| 参数名      | 类型     | 必填   | 参数描述             |
| -------- | ------ | ---- | ---------------- |
| propName | string | 是    | AppStorage中的属性名。 |

**返回值：**

| 类型                                  | 描述                                       |
| ----------------------------------- | ---------------------------------------- |
| SubscribedAbstractProperty&lt;T&gt; | 返回单向绑定的数据，如果AppStorage不存在对应的propName，则返回undefined。 |


```ts
AppStorage.setOrCreate('PropA', 47);
let prop1: SubscribedAbstractProperty<number> = AppStorage.prop('PropA');
let prop2: SubscribedAbstractProperty<number> = AppStorage.prop('PropA');
prop1.set(1); // one-way sync: prop1.get()=1; but prop2.get() == 47
```


### setAndProp<sup>10+</sup>

static setAndProp&lt;T&gt;(propName: string, defaultValue: T): SubscribedAbstractProperty&lt;T&gt;

与Prop接口类似。如果给定的propName在AppStorage存在，则返回该propName对应的属性的单向绑定数据。如果不存在，则使用defaultValue在AppStorage创建和初始化propName对应的属性，返回其单向绑定数据。


**参数：**

| 参数名          | 类型     | 必填   | 参数描述                                     |
| ------------ | ------ | ---- | ---------------------------------------- |
| propName     | string | 是    | AppStorage中的属性名。                         |
| defaultValue | T      | 是    | 当propName在AppStorage中不存在时，使用default在AppStorage中初始化对应的propName。 |

**返回值：**

| 类型                                  | 描述                                      |
| ----------------------------------- | --------------------------------------- |
| SubscribedAbstractProperty&lt;T&gt; | SubscribedAbstractProperty&lt;T&gt;的实例。 |


```ts
AppStorage.setOrCreate('PropA', 47);
let prop: SubscribedAbstractProperty<number> = AppStorage.setAndProp('PropB', 49); // PropA -> 47, PropB -> 49
```


### has<sup>10+</sup>

static has(propName: string): boolean

判断propName对应的属性是否在AppStorage中存在。

**参数：**

| 参数名      | 类型     | 必填   | 参数描述             |
| -------- | ------ | ---- | ---------------- |
| propName | string | 是    | AppStorage中的属性名。 |

**返回值：**

| 类型      | 描述                                       |
| ------- | ---------------------------------------- |
| boolean | 如果propName对应的属性在AppStorage中存在，则返回true。不存在则返回false。 |


```ts
AppStorage.has('simpleProp');
```


### get<sup>10+</sup>

static get&lt;T&gt;(propName: string): T | undefined

获取propName在AppStorage中对应的属性。如果不存在返回undefined。

**参数：**

| 参数名      | 类型     | 必填   | 参数描述             |
| -------- | ------ | ---- | ---------------- |
| propName | string | 是    | AppStorage中的属性名。 |

**返回值：**

| 类型                       | 描述                                       |
| ------------------------ | ---------------------------------------- |
| T&nbsp;\|&nbsp;undefined | AppStorage中propName对应的属性，如果不存在返回undefined。 |


```ts
AppStorage.setOrCreate('PropA', 47);
let value: number = AppStorage.get('PropA'); // 47
```


### set<sup>10+</sup>

static set&lt;T&gt;(propName: string, newValue: T): boolean

在AppStorage中设置propName对应属性的值。

**参数：**

| 参数名      | 类型     | 必填   | 参数描述                   |
| -------- | ------ | ---- | ---------------------- |
| propName | string | 是    | AppStorage中的属性名。       |
| newValue | T      | 是    | 属性值，不能为undefined或null。 |

**返回值：**

| 类型      | 描述                                       |
| ------- | ---------------------------------------- |
| boolean | 如果AppStorage不存在propName对应的属性，或者设置的newValue是undefined或者null，返回false。设置成功则返回true。 |


```ts
AppStorage.setOrCreate('PropA', 48);
let res: boolean = AppStorage.set('PropA', 47) // true
let res1: boolean = AppStorage.set('PropB', 47) // false
```


### setOrCreate<sup>10+</sup>

static setOrCreate&lt;T&gt;(propName: string, newValue: T): void

propName如果已经在AppStorage中存在，则设置propName对应是属性的值为newValue。如果不存在，则创建propName属性，值为newValue。

**参数：**

| 参数名      | 类型     | 必填   | 参数描述                   |
| -------- | ------ | ---- | ---------------------- |
| propName | string | 是    | AppStorage中的属性名。       |
| newValue | T      | 是    | 属性值，不能为undefined或null。 |


```ts
AppStorage.setOrCreate('simpleProp', 121);
```


### delete<sup>10+</sup>

static delete(propName: string): boolean

在AppStorage中删除propName对应的属性。

在AppStorage中删除该属性的前提是必须保证该属性没有订阅者。如果有订阅者，则返回false。删除成功返回true。

属性的订阅者为Link、Prop等接口绑定的propName，以及\@StorageLink('propName')和\@StorageProp('propName')。这就意味着如果自定义组件中使用\@StorageLink('propName')和\@StorageProp('propName')或者SubscribedAbstractProperty实例依旧对propName有同步关系，则该属性不能从AppStorage中删除。

**参数：**

| 参数名      | 类型     | 必填   | 参数描述             |
| -------- | ------ | ---- | ---------------- |
| propName | string | 是    | AppStorage中的属性名。 |

**返回值：**

| 类型      | 描述                                       |
| ------- | ---------------------------------------- |
| boolean | 如果AppStorage中有对应的属性，且该属性已经没有订阅者，则删除成功，返回true。如果属性不存在，或者该属性还存在订阅者，则返回false。 |


```ts
AppStorage.setOrCreate('PropA', 47);
AppStorage.link('PropA');
let res: boolean = AppStorage.delete('PropA'); // false, PropA still has a subscriber

AppStorage.setOrCreate('PropB', 48);
let res1: boolean = AppStorage.delete('PropB'); // true, PropB is deleted from AppStorage successfully
```


### keys<sup>10+</sup>

static keys(): IterableIterator&lt;string&gt;

返回AppStorage中所有的属性名。

**返回值：**

| 类型                             | 描述                 |
| ------------------------------ | ------------------ |
| IterableIterator&lt;string&gt; | AppStorage中所有的属性名。 |


```ts
AppStorage.setOrCreate('PropB', 48);
let keys: IterableIterator<string> = AppStorage.keys();
```


### clear<sup>10+</sup>

static clear(): boolean

清除AppStorage的所有的属性。在AppStorage中清除所有属性的前提是，已经没有任何订阅者。如果有，则什么都不做返回false；删除成功返回true。

订阅者的含义和参考[Delete](#delete)。

**返回值：**

| 类型      | 描述                                       |
| ------- | ---------------------------------------- |
| boolean | 如果AppStorage中的属性已经没有订阅者，则清除成功，返回true。否则返回false。 |


```ts
AppStorage.setOrCreate('PropA', 47);
let res: boolean = AppStorage.clear(); // true, there are no subscribers
```


### size<sup>10+</sup>

static size(): number

返回AppStorage中的属性数量。

**返回值：**

| 类型     | 描述                  |
| ------ | ------------------- |
| number | 返回AppStorage中属性的数量。 |


```ts
AppStorage.setOrCreate('PropB', 48);
let res: number = AppStorage.size(); // 1
```


### Link<sup>(deprecated)</sup>

static Link(propName: string): any

与AppStorage中对应的propName建立双向数据绑定。如果给定的propName在AppStorage中存在，返回与AppStorage中propName对应属性的双向绑定数据。

双向绑定数据的修改会同步回AppStorage中，AppStorage会将变化同步到所有绑定该propName的数据和自定义组件中。

如果AppStorage中不存在propName，则返回undefined。

从API version 10开始废弃，推荐使用[link10+](#link10)。


**参数：**

| 参数名      | 类型     | 必填   | 参数描述             |
| -------- | ------ | ---- | ---------------- |
| propName | string | 是    | AppStorage中的属性名。 |

**返回值：**

| 类型   | 描述                                       |
| ---- | ---------------------------------------- |
| any  | 返回双向绑定的数据，如果AppStorage不存在对应的propName，在返回undefined。 |


```ts
AppStorage.SetOrCreate('PropA', 47);
let linkToPropA1 = AppStorage.Link('PropA');
let linkToPropA2 = AppStorage.Link('PropA'); // linkToPropA2.get() == 47
linkToPropA1.set(48); // 双向同步: linkToPropA1.get() == linkToPropA2.get() == 48
```


### SetAndLink<sup>(deprecated)</sup>

static SetAndLink&lt;T&gt;(propName: string, defaultValue: T): SubscribedAbstractProperty&lt;T&gt;

与Link接口类似，如果给定的propName在AppStorage中存在，则返回该propName对应的属性的双向绑定数据。如果不存在，则使用defaultValue在AppStorage创建和初始化propName，返回其双向绑定数据。

从API version 10开始废弃，推荐使用[setAndLink10+](#setandlink10)。

**参数：**

| 参数名          | 类型     | 必填   | 参数描述                                     |
| ------------ | ------ | ---- | ---------------------------------------- |
| propName     | string | 是    | AppStorage中的属性名。                         |
| defaultValue | T      | 是    | 当propName在AppStorage中不存在，使用defaultValue在AppStorage中初始化对应的propName。 |

**返回值：**

| 类型                                  | 描述                                       |
| ----------------------------------- | ---------------------------------------- |
| SubscribedAbstractProperty&lt;T&gt; | SubscribedAbstractProperty&lt;T&gt;的实例，和AppStorage中propName对应属性的双向绑定的数据。 |


```ts
AppStorage.SetOrCreate('PropA', 47);
let link1: SubscribedAbstractProperty<number> = AppStorage.SetAndLink('PropB', 49); // Create PropB 49
let link2: SubscribedAbstractProperty<number> = AppStorage.SetAndLink('PropA', 50); // PropA exists, remains 47
```

### Prop<sup>(deprecated)</sup>

static Prop(propName: string): any

与AppStorage中对应的propName建立单向属性绑定。如果给定的propName在AppStorage中存在，则返回与AppStorage中propName对应属性的单向绑定数据。如果AppStorage中不存在propName，则返回undefined。单向绑定数据的修改不会被同步回AppStorage中。

>**说明：**
> Prop仅支持简单类型。
> 从API version 10开始废弃，推荐使用[prop10+](#prop10)。

**参数：**

| 参数名      | 类型     | 必填   | 参数描述             |
| -------- | ------ | ---- | ---------------- |
| propName | string | 是    | AppStorage中的属性名。 |

**返回值：**

| 类型   | 描述                                       |
| ---- | ---------------------------------------- |
| any  | 返回单向绑定的数据，如果AppStorage不存在对应的propName，则返回undefined。 |


```ts
AppStorage.SetOrCreate('PropA', 47);
let prop1 = AppStorage.Prop('PropA');
let prop2 = AppStorage.Prop('PropA');
prop1.set(1); // one-way sync: prop1.get()=1; but prop2.get() == 47
```


### SetAndProp<sup>(deprecated)</sup>

static SetAndProp&lt;S&gt;(propName: string, defaultValue: S): SubscribedAbstractProperty&lt;S&gt;

与Prop接口类似。如果给定的propName在AppStorage存在，则返回该propName对应的属性的单向绑定数据。如果不存在，则使用defaultValue在AppStorage创建和初始化propName对应的属性，返回其单向绑定数据。

从API version 10开始废弃，推荐使用[setAndProp10+](#setandprop10)。

**参数：**

| 参数名          | 类型     | 必填   | 参数描述                                     |
| ------------ | ------ | ---- | ---------------------------------------- |
| propName     | string | 是    | AppStorage中的属性名。                         |
| defaultValue | S      | 是    | 当propName在AppStorage中不存在时，使用default在AppStorage中初始化对应的propName。 |

**返回值：**

| 类型                                  | 描述                                      |
| ----------------------------------- | --------------------------------------- |
| SubscribedAbstractProperty&lt;S&gt; | SubscribedAbstractProperty&lt;S&gt;的实例。 |


```ts
AppStorage.SetOrCreate('PropA', 47);
let prop: SubscribedAbstractProperty<number> = AppStorage.SetAndProp('PropB', 49); // PropA -> 47, PropB -> 49
```


### Has<sup>(deprecated)</sup>

static Has(propName: string): boolean

判断propName对应的属性是否在AppStorage中存在。

从API version 10开始废弃，推荐使用[has10+](#has10)。

**参数：**

| 参数名      | 类型     | 必填   | 参数描述             |
| -------- | ------ | ---- | ---------------- |
| propName | string | 是    | AppStorage中的属性名。 |

**返回值：**

| 类型      | 描述                                       |
| ------- | ---------------------------------------- |
| boolean | 如果propName对应的属性在AppStorage中存在，则返回true。不存在则返回false。 |


```ts
AppStorage.Has('simpleProp');
```


### Get<sup>(deprecated)</sup>

static Get&lt;T&gt;(propName: string): T | undefined

获取propName在AppStorage中对应的属性。如果不存在返回undefined。

从API version 10开始废弃，推荐使用[get10+](#get10)。

**参数：**

| 参数名      | 类型     | 必填   | 参数描述             |
| -------- | ------ | ---- | ---------------- |
| propName | string | 是    | AppStorage中的属性名。 |

**返回值：**

| 类型                       | 描述                                       |
| ------------------------ | ---------------------------------------- |
| T&nbsp;\|&nbsp;undefined | AppStorage中propName对应的属性，如果不存在返回undefined。 |


```ts
AppStorage.SetOrCreate('PropA', 47);
let value: number = AppStorage.Get('PropA'); // 47
```


### Set<sup>(deprecated)</sup>

static Set&lt;T&gt;(propName: string, newValue: T): boolean

在AppStorage中设置propName对应属性的值。

从API version 10开始废弃，推荐使用[set10+](#set10)。

**参数：**

| 参数名      | 类型     | 必填   | 参数描述                   |
| -------- | ------ | ---- | ---------------------- |
| propName | string | 是    | AppStorage中的属性名。       |
| newValue | T      | 是    | 属性值，不能为undefined或null。 |

**返回值：**

| 类型      | 描述                                       |
| ------- | ---------------------------------------- |
| boolean | 如果AppStorage不存在propName对应的属性，或者设置的newValue是undefined或者null，返回false。设置成功则返回true。 |


```ts
AppStorage.SetOrCreate('PropA', 48);
let res: boolean = AppStorage.Set('PropA', 47) // true
let res1: boolean = AppStorage.Set('PropB', 47) // false
```


### SetOrCreate<sup>(deprecated)</sup>

static SetOrCreate&lt;T&gt;(propName: string, newValue: T): void

propName如果已经在AppStorage中存在，则设置propName对应是属性的值为newValue。如果不存在，则创建propName属性，值为newValue。

从API version 10开始废弃，推荐使用[setOrCreate10+](#setorcreate10)。

**参数：**

| 参数名      | 类型     | 必填   | 参数描述                   |
| -------- | ------ | ---- | ---------------------- |
| propName | string | 是    | AppStorage中的属性名。       |
| newValue | T      | 是    | 属性值，不能为undefined或null。 |


```ts
AppStorage.SetOrCreate('simpleProp', 121);
```


### Delete<sup>(deprecated)</sup>

static Delete(propName: string): boolean

在AppStorage中删除propName对应的属性。

在AppStorage中删除该属性的前提是必须保证该属性没有订阅者。如果有订阅者，则返回false。删除成功返回true。

属性的订阅者为Link、Prop等接口绑定的propName，以及\@StorageLink('propName')和\@StorageProp('propName')。这就意味着如果自定义组件中使用\@StorageLink('propName')和\@StorageProp('propName')或者SubscribedAbstractProperty实例依旧对propName有同步关系，则该属性不能从AppStorage中删除。

从API version 10开始废弃，推荐使用[delete10+](#delete10)。

**参数：**

| 参数名      | 类型     | 必填   | 参数描述             |
| -------- | ------ | ---- | ---------------- |
| propName | string | 是    | AppStorage中的属性名。 |

**返回值：**

| 类型      | 描述                                       |
| ------- | ---------------------------------------- |
| boolean | 如果AppStorage中有对应的属性，且该属性已经没有订阅者，则删除成功，返回true。如果属性不存在，或者该属性还存在订阅者，则返回false。 |


```ts
AppStorage.SetOrCreate('PropA', 47);
AppStorage.Link('PropA');
let res: boolean = AppStorage.Delete('PropA'); // false, PropA still has a subscriber

AppStorage.SetOrCreate('PropB', 48);
let res1: boolean = AppStorage.Delete('PropB'); // true, PropB is deleted from AppStorage successfully
```


### Keys<sup>(deprecated)</sup>

static Keys(): IterableIterator&lt;string&gt;

返回AppStorage中所有的属性名。

从API version 10开始废弃，推荐使用[keys10+](#keys10)。

**返回值：**

| 类型                             | 描述                 |
| ------------------------------ | ------------------ |
| IterableIterator&lt;string&gt; | AppStorage中所有的属性名。 |


```ts
AppStorage.SetOrCreate('PropB', 48);
let keys: IterableIterator<string> = AppStorage.Keys();
```


### staticClear<sup>(deprecated)</sup>

static staticClear(): boolean

删除所有的属性。

从API version 9开始废弃，推荐使用[Clear9+](#clear9)。

**返回值：**

| 类型      | 描述                                |
| ------- | --------------------------------- |
| boolean | 删除所有的属性，如果当前有状态变量依旧引用此属性，返回false。 |


```ts
let simple = AppStorage.staticClear();
```


### Clear<sup>(deprecated)</sup>

static Clear(): boolean

清除AppStorage的所有的属性。在AppStorage中清除所有属性的前提是，已经没有任何订阅者。如果有，则什么都不做返回false；删除成功返回true。

订阅者的含义和参考[Delete](#delete)。

从API version 10开始废弃，推荐使用[clear10+](#clear10)。

**返回值：**

| 类型      | 描述                                       |
| ------- | ---------------------------------------- |
| boolean | 如果AppStorage中的属性已经没有订阅者，则清除成功，返回true。否则返回false。 |


```typescript
AppStorage.SetOrCreate('PropA', 47);
let res: boolean = AppStorage.Clear(); // true, there are no subscribers
```


### IsMutable<sup>(deprecated)</sup>

static IsMutable(propName: string): boolean

返回AppStorage中propName对应的属性是否是可变的。

从API version 10开始废弃。

**参数：**

| 参数名      | 类型     | 必填   | 参数描述             |
| -------- | ------ | ---- | ---------------- |
| propName | string | 是    | AppStorage中的属性名。 |

**返回值：**

| 类型      | 描述                               |
| ------- | -------------------------------- |
| boolean | 返回AppStorage中propNam对应的属性是否是可变的。 |


```ts
AppStorage.SetOrCreate('PropA', 47);
let res: boolean = AppStorage.IsMutable('simpleProp');
```


### Size<sup>(deprecated)</sup>

static Size(): number

返回AppStorage中的属性数量。

从API version 10开始废弃，推荐使用[size10+](#size10)。

**返回值：**

| 类型     | 描述                  |
| ------ | ------------------- |
| number | 返回AppStorage中属性的数量。 |


```ts
AppStorage.SetOrCreate('PropB', 48);
let res: number = AppStorage.Size(); // 1
```


## LocalStorage<sup>9+</sup>


### constructor<sup>9+</sup>

constructor(initializingProperties?: Object)

创建一个新的LocalStorage实例。使用Object.keys(initializingProperties)返回的属性和其数值，初始化LocalStorage实例。

从API version 9开始，该接口支持在ArkTS卡片中使用。

**参数：**

| 参数名                    | 类型     | 必填   | 参数描述                                     |
| ---------------------- | ------ | ---- | ---------------------------------------- |
| initializingProperties | Object | 否    | 用initializingProperties包含的属性和数值初始化LocalStorage。initializingProperties不能为undefined。 |


```ts
let storage: LocalStorage = new LocalStorage({ 'PropA': 47 });
```


### getShared<sup>10+</sup>

static getShared(): LocalStorage

获取当前stage共享的LocalStorage实例。

从API version 9开始，该接口支持在ArkTS卡片中使用。

**模型约束：**此接口仅可在Stage模型下使用。

**返回值：**

| 类型                             | 描述                |
| ------------------------------ | ----------------- |
| [LocalStorage](#localstorage9) | 返回LocalStorage实例。 |


```ts
let storage: LocalStorage = LocalStorage.getShared();
```


### has<sup>9+</sup>

has(propName: string): boolean

判断propName对应的属性是否在LocalStorage中存在。

从API version 9开始，该接口支持在ArkTS卡片中使用。

**参数：**

| 参数名      | 类型     | 必填   | 参数描述               |
| -------- | ------ | ---- | ------------------ |
| propName | string | 是    | LocalStorage中的属性名。 |

**返回值：**

| 类型      | 描述                                       |
| ------- | ---------------------------------------- |
| boolean | 如果propName对应的属性在AppStorage中存在，则返回true。不存在则返回false。 |


```
let storage: LocalStorage = new LocalStorage({ 'PropA': 47 });
storage.has('PropA'); // true
```


### get<sup>9+</sup>

get&lt;T&gt;(propName: string): T | undefined

获取propName在LocalStorage中对应的属性。

从API version 9开始，该接口支持在ArkTS卡片中使用。

**参数：**

| 参数名      | 类型     | 必填   | 参数描述               |
| -------- | ------ | ---- | ------------------ |
| propName | string | 是    | LocalStorage中的属性名。 |

**返回值：**

| 类型                       | 描述                                       |
| ------------------------ | ---------------------------------------- |
| T&nbsp;\|&nbsp;undefined | LocalStorage中propName对应的属性，如果不存在返回undefined。 |


```ts
let storage: LocalStorage = new LocalStorage({ 'PropA': 47 });
let value: number = storage.get('PropA'); // 47
```


### set<sup>9+</sup>

set&lt;T&gt;(propName: string, newValue: T): boolean

在LocalStorage中设置propName对应属性的值。

从API version 9开始，该接口支持在ArkTS卡片中使用。

**参数：**

| 参数名      | 类型     | 必填   | 参数描述                    |
| -------- | ------ | ---- | ----------------------- |
| propName | string | 是    | LocalStorage中的属性名。      |
| newValue | T      | 是    | 属性值，不能为undefined或者null。 |

**返回值：**

| 类型      | 描述                                       |
| ------- | ---------------------------------------- |
| boolean | 如果LocalStorage不存在propName对应的属性，或者设置的newValue是undefined或者null，返回false。设置成功返回true。 |


```ts
let storage: LocalStorage = new LocalStorage({ 'PropA': 47 });
let res: boolean = storage.set('PropA', 47); // true
let res1: boolean = storage.set('PropB', 47); // false
```


### setOrCreate<sup>9+</sup>

setOrCreate&lt;T&gt;(propName: string, newValue: T): boolean

propName如果已经在LocalStorage中存在，则设置propName对应是属性的值为newValue。如果不存在，则创建propName属性，初始化为newValue。

从API version 9开始，该接口支持在ArkTS卡片中使用。

**参数：**

| 参数名      | 类型     | 必填   | 参数描述                    |
| -------- | ------ | ---- | ----------------------- |
| propName | string | 是    | LocalStorage中的属性名。      |
| newValue | T      | 是    | 属性值，不能为undefined或者null。 |

**返回值：**

| 类型      | 描述                                       |
| ------- | ---------------------------------------- |
| boolean | 如果设置的newValue是undefined或者null，返回false。<br/>如果LocalStorage存在propName，则更新其值为newValue，返回true。<br/>如果LocalStorage不存在propName，则创建propName，并初始化其值为newValue，返回true。 |


```ts
let storage: LocalStorage = new LocalStorage({ 'PropA': 47 });
let res: boolean =storage.setOrCreate('PropA', 121); // true
let res1: boolean =storage.setOrCreate('PropB', 111); // true
let res2: boolean =storage.setOrCreate('PropB', undefined); // false
```


### link<sup>9+</sup>

link&lt;T&gt;(propName: string): SubscribedAbstractProperty&lt;T&gt;

如果给定的propName在LocalStorage实例中存在，则返回与LocalStorage中propName对应属性的双向绑定数据。

双向绑定数据的修改会被同步回LocalStorage中，LocalStorage会将变化同步到所有绑定该propName的数据和Component中。

如果LocalStorage中不存在propName，则返回undefined。

从API version 9开始，该接口支持在ArkTS卡片中使用。

**参数：**

| 参数名      | 类型     | 必填   | 参数描述               |
| -------- | ------ | ---- | ------------------ |
| propName | string | 是    | LocalStorage中的属性名。 |

**返回值：**

| 类型                                  | 描述                                       |
| ----------------------------------- | ---------------------------------------- |
| SubscribedAbstractProperty&lt;T&gt; | SubscribedAbstractProperty&lt;T&gt;的实例，如果AppStorage不存在对应的propName，再返回undefined。 |


```ts
let storage: LocalStorage = new LocalStorage({ 'PropA': 47 });
let linkToPropA1: SubscribedAbstractProperty<number> = storage.link('PropA');
let linkToPropA2: SubscribedAbstractProperty<number> = storage.link('PropA'); // linkToPropA2.get() == 47
linkToPropA1.set(48); // 双向同步: linkToPropA1.get() == linkToPropA2.get() == 48
```


### setAndLink<sup>9+</sup>

setAndLink&lt;T&gt;(propName: string, defaultValue: T): SubscribedAbstractProperty&lt;T&gt;

与Link接口类似，如果给定的propName在LocalStorage存在，则返回该propName对应的属性的双向绑定数据。如果不存在，则使用defaultValue在LocalStorage创建和初始化propName，返回其双向绑定数据。

从API version 9开始，该接口支持在ArkTS卡片中使用。

**参数：**

| 参数名          | 类型     | 必填   | 参数描述                                     |
| ------------ | ------ | ---- | ---------------------------------------- |
| propName     | string | 是    | LocalStorage中的属性名。                       |
| defaultValue | T      | 是    | 当propName在LocalStorage中不存在，使用default在LocalStorage中初始化对应的propName。 |

**返回值：**

| 类型                                  | 描述                                       |
| ----------------------------------- | ---------------------------------------- |
| SubscribedAbstractProperty&lt;T&gt; | SubscribedAbstractProperty&lt;T&gt;的实例，如果AppStorage不存在对应的propName，再返回undefined。 |


```ts
let storage: LocalStorage = new LocalStorage({ 'PropA': 47 });
let link1: SubscribedAbstractProperty<number> = storage.setAndLink('PropB', 49); // Create PropB 49
var link2: SubscribedAbstractProperty<number> = storage.setAndLink('PropA', 50); // PropA exists, remains 47
```


### prop<sup>9+</sup>

prop&lt;S&gt;(propName: string): SubscribedAbstractProperty&lt;S&gt;

如果给定的propName在LocalStorage存在，则返回与LocalStorage中propName对应属性的单向绑定数据。如果LocalStorage中不存在propName，则返回undefined。单向绑定数据的修改不会被同步回LocalStorage中。

从API version 9开始，该接口支持在ArkTS卡片中使用。

**参数：**

| 参数名      | 类型     | 必填   | 参数描述               |
| -------- | ------ | ---- | ------------------ |
| propName | string | 是    | LocalStorage中的属性名。 |

**返回值：**

| 类型                                  | 描述                                       |
| ----------------------------------- | ---------------------------------------- |
| SubscribedAbstractProperty&lt;S&gt; | SubscribedAbstractProperty&lt;S&gt;的实例，如果AppStorage不存在对应的propName，在返回undefined。 |


```ts
let storage: LocalStorage = new LocalStorage({ 'PropA': 47 });
let prop1: SubscribedAbstractProperty<number> = storage.prop('PropA');
let prop2: SubscribedAbstractProperty<number> = storage.prop('PropA');
prop1.set(1); // one-way sync: prop1.get()=1; but prop2.get() == 47
```


### setAndProp<sup>9+</sup>

setAndProp&lt;S&gt;(propName: string, defaultValue: S): SubscribedAbstractProperty&lt;S&gt;

propName在LocalStorage存在，则返回该propName对应的属性的单向绑定数据。如果不存在，则使用defaultValue在LocalStorage创建和初始化propName对应的属性，返回其单向绑定数据。

从API version 9开始，该接口支持在ArkTS卡片中使用。

**参数：**

| 参数名          | 类型     | 必填   | 参数描述                                     |
| ------------ | ------ | ---- | ---------------------------------------- |
| propName     | string | 是    | LocalStorage中的属性名。                       |
| defaultValue | S      | 是    | 当propName在AppStorage中不存在，使用default在AppStorage中初始化对应的propName。 |

**返回值：**

| 类型                                  | 描述                                       |
| ----------------------------------- | ---------------------------------------- |
| SubscribedAbstractProperty&lt;S&gt; | SubscribedAbstractProperty&lt;S&gt;的实例，和AppStorage中propName对应属性的单向绑定的数据。 |


```ts
let storage: LocalStorage = new LocalStorage({ 'PropA': 47 });
let prop: SubscribedAbstractProperty<number> = storage.setAndProp('PropB', 49); // PropA -> 47, PropB -> 49
```


### delete<sup>9+</sup>

delete(propName: string): boolean

在LocalStorage中删除propName对应的属性。删除属性的前提是该属性已经没有订阅者，如果有则返回false。删除成功则返回true。

属性的订阅者是link，prop接口绑定的propName，以及\@LocalStorageLink('propName')和\@LocalStorageProp('propName')。如果自定义组件Component中使用或者SubscribedAbstractProperty（link和prop接口的返回类型）依旧有同步关系，则该属性不能从LocalStorage中删除。

从API version 9开始，该接口支持在ArkTS卡片中使用。

**参数：**

| 参数名      | 类型     | 必填   | 参数描述               |
| -------- | ------ | ---- | ------------------ |
| propName | string | 是    | LocalStorage中的属性名。 |

**返回值：**

| 类型      | 描述                                       |
| ------- | ---------------------------------------- |
| boolean | 如果LocalStorage中有对应的属性，且该属性已经没有订阅者，则删除成功返回true。如果属性不存在，或者该属性还存在订阅者，则返回false。 |


```ts
let storage: LocalStorage = new LocalStorage({ 'PropA': 47 });
storage.link('PropA');
let res: boolean = storage.delete('PropA'); // false, PropA still has a subscriber
let res1: boolean = storage.delete('PropB'); // false, PropB is not in storage
storage.setOrCreate('PropB', 48);
let res2: boolean = storage.delete('PropB'); // true, PropB is deleted from storage successfully
```


### keys<sup>9+</sup>

keys(): IterableIterator&lt;string&gt;

返回AppStorage中所有的属性名。

从API version 9开始，该接口支持在ArkTS卡片中使用。

**返回值：**

| 类型                             | 描述                   |
| ------------------------------ | -------------------- |
| IterableIterator&lt;string&gt; | LocalStorage中所有的属性名。 |


```ts
let storage: LocalStorage = new LocalStorage({ 'PropA': 47 });
let keys: IterableIterator<string> = storage.keys();
```


### size<sup>9+</sup>

size(): number

返回LocalStorage中的属性数量。

从API version 9开始，该接口支持在ArkTS卡片中使用。

**返回值：**

| 类型     | 描述        |
| ------ | --------- |
| number | 返回键值对的数量。 |


```ts
let storage: LocalStorage = new LocalStorage({ 'PropA': 47 });
let res: number = storage.size(); // 1
```


### clear<sup>9+</sup>

clear(): boolean


清除LocalStorage的所有的属性。在LocalStorage中清除所有属性的前提是已经没有任何订阅者。如果有则返回false；清除成功返回true。

从API version 9开始，该接口支持在ArkTS卡片中使用。

**返回值：**


| 类型      | 描述                                       |
| ------- | ---------------------------------------- |
| boolean | 如果LocalStorage中的属性已经没有任何订阅者，则清除成功，返回true。否则返回false。 |



```ts
let storage: LocalStorage = new LocalStorage({ 'PropA': 47 });
let res: boolean = storage.clear(); // true, there are no subscribers
```


### GetShared<sup>(deprecated)</sup>

static GetShared(): LocalStorage

获取当前stage共享的LocalStorage实例。

从API version 9开始，该接口支持在ArkTS卡片中使用。

从API version 10开始废弃，推荐使用[getShared10+](#getshared10)。

**模型约束：**此接口仅可在Stage模型下使用。

**返回值：**

| 类型                             | 描述                |
| ------------------------------ | ----------------- |
| [LocalStorage](#localstorage9) | 返回LocalStorage实例。 |


```ts
let storage: LocalStorage = LocalStorage.GetShared();
```


## SubscribedAbstractProperty


### get<sup>9+</sup>

abstract get(): T

读取从AppStorage/LocalStorage同步属性的数据。

从API version 9开始，该接口支持在ArkTS卡片中使用。

**返回值：**

| 类型   | 描述                              |
| ---- | ------------------------------- |
| T    | AppStorage/LocalStorage同步属性的数据。 |


```ts
AppStorage.SetOrCreate('PropA', 47); 
let prop1 = AppStorage.Prop('PropA');    
prop1.get(); //  prop1.get()=47
```


### set<sup>9+</sup>

abstract set(newValue: T): void

设置AppStorage/LocalStorage同步属性的数据。

从API version 9开始，该接口支持在ArkTS卡片中使用。


**参数：**


| 参数名      | 类型   | 必填   | 参数描述    |
| -------- | ---- | ---- | ------- |
| newValue | T    | 是    | 要设置的数据。 |



```
AppStorage.SetOrCreate('PropA', 47);
let prop1 = AppStorage.Prop('PropA');
prop1.set(1); //  prop1.get()=1
```

### aboutToBeDeleted<sup>10+</sup>

abstract aboutToBeDeleted(): void

取消SubscribedAbstractProperty实例对AppStorage/LocalStorage单/双向同步关系。


```ts
AppStorage.SetOrCreate('PropA', 47);
let link = AppStorage.SetAndLink('PropB', 49); // PropA -> 47, PropB -> 49
link.aboutToBeDeleted();
link.set(50); // PropB -> 49, link.get() --> undefined
```


## PersistentStorage

### PersistPropsOptions

| 参数名       | 类型                    | 必填 | 参数描述                                                     |
| ------------ | ----------------------- | ---- | ------------------------------------------------------------ |
| key          | string                  | 是   | 属性名。                                                     |
| defaultValue | number\|string\|boolean | 是   | 在PersistentStorage和AppStorage未查询到时，则使用默认值初始化初始化它。不允许为undefined和null。 |


### persistProp<sup>10+</sup>

static persistProp&lt;T&gt;(key: string, defaultValue: T): void

将AppStorage中key对应的属性持久化到文件中。该接口的调用通常在访问AppStorage之前。

确定属性的类型和值的顺序如下：

1. 如果PersistentStorage文件中存在key对应的属性，在AppStorage中创建对应的propName，并用在PersistentStorage中找到的key的属性初始化。

2. 如果PersistentStorage文件中没有查询到key对应的属性，则在AppStorage中查找key对应的属性。如果找到key对应的属性，则将该属性持久化。

3. 如果AppStorage也没查找到key对应的属性，则在AppStorage中创建key对应的属性。用defaultValue初始化其值，并将该属性持久化。

根据上述的初始化流程，如果AppStorage中有该属性，则会使用其值，覆盖掉PersistentStorage文件中的值。由于AppStorage是内存内数据，该行为会导致数据丧失持久化能力。

**参数：**

| 参数名          | 类型     | 必填   | 参数描述                                     |
| ------------ | ------ | ---- | ---------------------------------------- |
| key          | string | 是    | 属性名。                                     |
| defaultValue | T      | 是    | 在PersistentStorage和AppStorage未查询到时，则使用默认值初始化初始化它。不允许为undefined和null。 |


**示例：**


```ts
PersistentStorage.persistProp('highScore', '0');
```


### deleteProp<sup>10+</sup>

static deleteProp(key: string): void

PersistProp的逆向操作。将key对应的属性从PersistentStorage删除，后续AppStorage的操作，对PersistentStorage不会再有影响。

**参数：**

| 参数名  | 类型     | 必填   | 参数描述                    |
| ---- | ------ | ---- | ----------------------- |
| key  | string | 是    | PersistentStorage中的属性名。 |


```ts
PersistentStorage.deleteProp('highScore');
```


### persistProps<sup>10+</sup>

static persistProps(props: PersistPropsOptions[]): void

行为和PersistProp类似，不同在于可以一次性持久化多个数据，适合在应用启动的时候初始化。

**参数：**

| 参数名        | 类型                                       | 必填   | 参数描述                                     |
| ---------- | ---------------------------------------- | ---- | ---------------------------------------- |
| props | [PersistPropsOptions](#persistpropsoptions)[] | 是 | 持久化数组。 |


```ts
PersistentStorage.persistProps([{ key: 'highScore', defaultValue: '0' }, { key: 'wightScore', defaultValue: '1' }]);
```


### keys<sup>10+</sup>

static keys(): Array&lt;string&gt;

返回所有持久化属性的key的数组。

**返回值：**

| 类型                  | 描述                |
| ------------------- | ----------------- |
| Array&lt;string&gt; | 返回所有持久化属性的key的数组。 |


```ts
let keys: Array<string> = PersistentStorage.keys();
```


### PersistProp<sup>(deprecated)</sup>

static PersistProp&lt;T&gt;(key: string, defaultValue: T): void

将AppStorage中key对应的属性持久化到文件中。该接口的调用通常在访问AppStorage之前。

确定属性的类型和值的顺序如下：

1. 如果PersistentStorage文件中存在key对应的属性，在AppStorage中创建对应的propName，并用在PersistentStorage中找到的key的属性初始化。

2. 如果PersistentStorage文件中没有查询到key对应的属性，则在AppStorage中查找key对应的属性。如果找到key对应的属性，则将该属性持久化。

3. 如果AppStorage也没查找到key对应的属性，则在AppStorage中创建key对应的属性。用defaultValue初始化其值，并将该属性持久化。

根据上述的初始化流程，如果AppStorage中有该属性，则会使用其值，覆盖掉PersistentStorage文件中的值。由于AppStorage是内存内数据，该行为会导致数据丧失持久化能力。

从API version 10开始废弃，推荐使用[persistProp10+](#persistprop10)。

**参数：**

| 参数名          | 类型     | 必填   | 参数描述                                     |
| ------------ | ------ | ---- | ---------------------------------------- |
| key          | string | 是    | 属性名。                                     |
| defaultValue | T      | 是    | 在PersistentStorage和AppStorage未查询到时，则使用默认值初始化初始化它。不允许为undefined和null。 |


**示例：**


```ts
PersistentStorage.PersistProp('highScore', '0');
```


### DeleteProp<sup>(deprecated)</sup>

static DeleteProp(key: string): void

PersistProp的逆向操作。将key对应的属性从PersistentStorage删除，后续AppStorage的操作，对PersistentStorage不会再有影响。

从API version 10开始废弃，推荐使用[deleteProp10+](#deleteprop10)。

**参数：**

| 参数名  | 类型     | 必填   | 参数描述                    |
| ---- | ------ | ---- | ----------------------- |
| key  | string | 是    | PersistentStorage中的属性名。 |


```ts
PersistentStorage.DeleteProp('highScore');
```


### PersistProps<sup>(deprecated)</sup>

static PersistProps(properties: {key: string, defaultValue: any;}[]): void

行为和PersistProp类似，不同在于可以一次性持久化多个数据，适合在应用启动的时候初始化。

从API version 10开始废弃，推荐使用[persistProps10+](#persistprops10)。

**参数：**

| 参数名     | 类型                                              | 必填 | 参数描述                                                     |
| ---------- | ------------------------------------------------- | ---- | ------------------------------------------------------------ |
| properties | {key:&nbsp;string,&nbsp;defaultValue:&nbsp;any}[] | 是   | 持久化数组，启动key为属性名，defaultValue为默认值。规则同PersistProp。 |


```ts
PersistentStorage.PersistProps([{ key: 'highScore', defaultValue: '0' }, { key: 'wightScore', defaultValue: '1' }]);
```


### Keys<sup>(deprecated)</sup>

static Keys(): Array&lt;string&gt;

返回所有持久化属性的key的数组。

从API version 10开始废弃，推荐使用[keys10+](#keys10-1)。

**返回值：**

| 类型                  | 描述                |
| ------------------- | ----------------- |
| Array&lt;string&gt; | 返回所有持久化属性的key的数组。 |


```ts
let keys: Array<string> = PersistentStorage.Keys();
```


## Environment


### EnvPropsOptions

| 参数名       | 类型                    | 必填 | 参数描述                                                     |
| ------------ | ----------------------- | ---- | ------------------------------------------------------------ |
| key          | string                  | 是   | 环境变量名称，支持的范围详见[内置环境变量说明](#内置环境变量说明)。 |
| defaultValue | number\|string\|boolean | 是   | 查询不到环境变量key，则使用defaultValue作为默认值存入AppStorage中。 |


### envProp<sup>10+</sup>

static envProp&lt;S&gt;(key: string, value: S): boolean

将Environment的内置环境变量key存入AppStorage中。如果系统中未查询到Environment环境变量key的值，则使用默认值value，存入成功，返回true。如果AppStorage已经有对应的key，则返回false。

所以建议在程序启动的时候调用该接口。

在没有调用EnvProp，就使用AppStorage读取环境变量是错误的。

**参数：**

| 参数名   | 类型     | 必填   | 参数描述                                    |
| ----- | ------ | ---- | --------------------------------------- |
| key   | string | 是    | 环境变量名称，支持的范围详见[内置环境变量说明](#内置环境变量说明)。    |
| value | S      | 是    | 查询不到环境变量key，则使用value作为默认值存入AppStorage中。 |

**返回值：**

| 类型      | 描述                                       |
| ------- | ---------------------------------------- |
| boolean | 如果key对应的属性在AppStorage中存在，则返回false。不存在则在AppStorage中创建key对应的属性，返回true。 |

**示例：**


```ts
Environment.envProp('accessibilityEnabled', 'default');
```


### 内置环境变量说明

| key                  | 类型              | 说明                                       |
| -------------------- | --------------- | ---------------------------------------- |
| accessibilityEnabled | string          | 无障碍屏幕朗读是否启用。                             |
| colorMode            | ColorMode       | 深浅色模式，可选值为：<br/>-&nbsp;ColorMode.LIGHT：浅色模式；<br/>-&nbsp;ColorMode.DARK：深色模式。 |
| fontScale            | number          | 字体大小比例。                                  |
| fontWeightScale      | number          | 字重比例。                                    |
| layoutDirection      | LayoutDirection | 布局方向类型，可选值为：<br/>-&nbsp;LayoutDirection.LTR：从左到右；<br/>-&nbsp;LayoutDirection.RTL：从右到左。 |
| languageCode         | string          | 当前系统语言，小写字母，例如zh。                        |


### envProps<sup>10+</sup>

static envProps(props: EnvPropsOptions[]): void

和EnvProp类似，不同点在于参数为数组，可以一次性初始化多个数据。建议在应用启动时调用，将系统环境变量批量存入AppStorage中。

**参数：**

| 参数名 | 类型                                          | 必填 | 参数描述                             |
| ------ | --------------------------------------------- | ---- | ------------------------------------ |
| props  | [EnvPropsOptions](#envpropsoptions)[] | 是   | 系统环境变量和默认值的键值对的数组。 |


```ts
Environment.envProps([{ key: 'accessibilityEnabled', defaultValue: 'default' }, {
  key: 'languageCode',
  defaultValue: 'en'
}, { key: 'prop', defaultValue: 'hhhh' }]);
```


### keys<sup>10+</sup>

static keys(): Array&lt;string&gt;

返回环境变量的属性key的数组。

**返回值：**

| 类型                  | 描述          |
| ------------------- | ----------- |
| Array&lt;string&gt; | 返回关联的系统项数组。 |


```ts
Environment.envProps([{ key: 'accessibilityEnabled', defaultValue: 'default' }, {
  key: 'languageCode',
  defaultValue: 'en'
}, { key: 'prop', defaultValue: 'hhhh' }]);

let keys: Array<string> = Environment.keys(); // accessibilityEnabled, languageCode, prop
```


### EnvProp<sup>(deprecated)</sup>

static EnvProp&lt;S&gt;(key: string, value: S): boolean

将Environment的内置环境变量key存入AppStorage中。如果系统中未查询到Environment环境变量key的值，则使用默认值value，存入成功，返回true。如果AppStorage已经有对应的key，则返回false。

所以建议在程序启动的时候调用该接口。

在没有调用EnvProp，就使用AppStorage读取环境变量是错误的。

从API version 10开始废弃，推荐使用[envProp10+](#envprop10)。

**参数：**

| 参数名   | 类型     | 必填   | 参数描述                                    |
| ----- | ------ | ---- | --------------------------------------- |
| key   | string | 是    | 环境变量名称，支持的范围详见[内置环境变量说明](#内置环境变量说明)。    |
| value | S      | 是    | 查询不到环境变量key，则使用value作为默认值存入AppStorage中。 |

**返回值：**

| 类型      | 描述                                       |
| ------- | ---------------------------------------- |
| boolean | 如果key对应的属性在AppStorage中存在，则返回false。不存在则在AppStorage中创建key对应的属性，返回true。 |

**示例：**


```ts
Environment.EnvProp('accessibilityEnabled', 'default');
```


### EnvProps<sup>(deprecated)</sup>

static EnvProps(props: {key: string; defaultValue: any;}[]): void

和EnvProp类似，不同点在于参数为数组，可以一次性初始化多个数据。建议在应用启动时调用，将系统环境变量批量存入AppStorage中。

从API version 10开始废弃，推荐使用[envProps10+](#envprops10)。

**参数：**

| 参数名   | 类型                                       | 必填   | 参数描述               |
| ----- | ---------------------------------------- | ---- | ------------------ |
| props | {key:&nbsp;string,&nbsp;defaultValue:&nbsp;any}[] | 是    | 系统环境变量和默认值的键值对的数组。 |


```ts
Environment.EnvProps([{ key: 'accessibilityEnabled', defaultValue: 'default' }, {
  key: 'languageCode',
  defaultValue: 'en'
}, { key: 'prop', defaultValue: 'hhhh' }]);
```


### Keys<sup>(deprecated)</sup>

static Keys(): Array&lt;string&gt;

返回环境变量的属性key的数组。

从API version 10开始废弃，推荐使用[keys10+](#keys10-2)。

**返回值：**

| 类型                  | 描述          |
| ------------------- | ----------- |
| Array&lt;string&gt; | 返回关联的系统项数组。 |


```ts
Environment.EnvProps([{ key: 'accessibilityEnabled', defaultValue: 'default' }, {
  key: 'languageCode',
  defaultValue: 'en'
}, { key: 'prop', defaultValue: 'hhhh' }]);

let keys: Array<string> = Environment.Keys(); // accessibilityEnabled, languageCode, prop
```