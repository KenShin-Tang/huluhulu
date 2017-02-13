# Optional Chaining

* optional chaining 是用来访问/调用  optional 的properties/methods/subscripts的处理过程.如果 optional 包含有值, 那么访问/调用就成功; 否则就返回 nil. 
* 由于在访问 optional 的properties/methods/subscripts 时我们不知道 optional 是否有值, 所以链式访问/调用就很难做到(因为 force unwrapping optional可能触发 runtime error);  那么我们就可以使用 optional chaining 方式做到. 在链式表达式中optional节点后放置一个`?`.

* 多级 chaining 可以串起来, 且不会给结果"添加"更多层次的 optionality, 即我们要访问的已经是一个 optional 了, 它不会因为我们多级 optional chaining 而增加一级 optional.
