### 1.1.2　Go与模块化Web应用

大规模Web应用应该由可替换的组件构成，这种做法能够使开发者更容易添加、移除或者修改特性，从而更好地满足程序不断变化的需求。除此之外，这种做法的另一个好处是使开发者可以通过复用模块化的组件来降低软件开发所需的费用。

尽管Go是一门静态类型语言，但用户可以通过它的接口机制对行为进行描述，以此来实现动态类型匹配（dynamic typing）。Go语言的函数可以接受接口作为参数，这意味着用户只要实现了接口所需的方法，就可以在继续使用现有代码的同时向系统中引入新的代码。与此同时，因为Go语言的所有类型都实现了空接口，所以用户只需要创建出一个接受空接口作为参数的函数，就可以把任何类型的值用作该函数的实际参数。此外，Go语言还实现了一些在函数式编程中非常常见的特性，其中包括函数类型、使用函数作为值以及闭包，这些特性允许用户使用已有的函数来构建新的函数，从而帮助用户构建出更为模块化的代码。

Go语言也经常会被用于创建微服务（microservice）。在微服务架构中，大型应用通常由多个规模较小的独立服务组合而成，这些独立服务通常可以相互替换，并根据它们各自的功能进行组织。比如，日志记录服务会被归类为系统级服务，而开具账单、风险分析这样的服务则会被归类为应用级服务。创建多个规模较小的Go服务并将它们组合为单个Web应用，这种做法使得我们可以在有需要的时候对应用中的服务进行替换，而整个Web应用也会因此变得更加模块化。

