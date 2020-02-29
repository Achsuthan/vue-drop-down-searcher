# vue-drop-down-searcher

Customisable dropdown select for Vue

<img src="https://badge.fury.io/js/vue-drop-down-searcher.svg" alt="version badge">


### &#x1F53A; Whats New

- Search porps added 
- Search filter added 
- InputChanged Call back pros uppercase removed
- Outside click event to dismiss the dropdown added

### Features

- Configurable via props
- Plugin is supportable for mouse outside click
- Auto position
- Small bundle size

### Installation

```sh
npm i vue-drop-down-searcher
```

### Website

[Demo](https://vue-dropdown-searcher.firebaseapp.com)
<br/>
[Npm Link](https://www.npmjs.com/package/vue-drop-down-searcher)

### Usage

Import :

```sh
import DropDown from "vue-drop-down-searcher";
```

and use as

```sh
<DropDown list={list} selectedList={selectedItem} toggleItem={val => toggleItem(val)} handleInputChange= {(val)=>handleInputChange(val)}/>
```

### API

Component Props

| Prop              | Type        | Default | Description                                                                                          |
| ----------------- | ----------- | ------- | ---------------------------------------------------------------------------------------------------- |
| list              | ArrayObject | []      | These array values will show in the dropdown                                                         |
| placeholder       | String      | Search  | Input field placeholder                                                                              |
| searchKey       | String      | Empty  | Search Key for filter 
| isSingle          | bool        | false   | if true, only one value can be selected from dropdown otherwise multi value can be selected dropdown |
| labelName         | String      | title   | This value used to show which value is from the object in dropdown                                   |
| selectedlabelName | String      | title   | From which value from the object need to show in the taginput                                        |
| selectedList      | ArrayOBject | []      | If values set, it will show those values as tag input                                                |

### Callback props

> by using render props to override components some of the functionality will have to be >handled manually with a help of internal props, states and methods exposed

| Prop         | Type | Default | Description                                            |
| ------------ | ---- | ------- | ------------------------------------------------------ |
| toggleItem   | func |         | This will return the selected values from dropdwon     |
| inputChanged | func |         | When type something from the textfiled it will trigger |

### Screenshots

- Main Image
  ![alt text](https://firebasestorage.googleapis.com/v0/b/npmplugins.appspot.com/o/main.png?alt=media&token=e6748fab-0087-41c1-9581-fcbb73a39fdf)
- Single Dropdown
  ![alt text](https://firebasestorage.googleapis.com/v0/b/npmplugins.appspot.com/o/singleSelect.png?alt=media&token=48f4424e-3e05-4587-972e-66ec597261d0)
- Multi Dropdown
  ![alt text](https://firebasestorage.googleapis.com/v0/b/npmplugins.appspot.com/o/multiSelect.png?alt=media&token=4f04b082-deaa-4647-bc94-23c0d8b8772d)
  License
  [MIT](https://github.com/Achsuthan/vue-drop-down-searcher/blob/master/LICENSE)

  <h3>Demo Gif</h3>
<img src="./screenshots/demo.gif"/>
<hr>
<a href = "mailto: achsuthan@icloud.com">Contact Me</a>
