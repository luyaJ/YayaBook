# Vuex

## namespaced 作用

vuex 中的 store 分模块管理，需要在 store 的 index.js 中引入各个模块，为了解决不同模块命名冲突的问题，我们使用 `namespaced: true`，之后