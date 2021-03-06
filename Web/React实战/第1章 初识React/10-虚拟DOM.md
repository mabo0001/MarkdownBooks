### 1.3.2　虚拟DOM

浏览器中的Web API让我们可以使用JavaScript通过DOM与Web文档进行交互。但如果我们已经能做到这一点，为什么在这之间还需要别的东西？首先我想说明的是，React实现虚拟DOM并不意味着常规Web API不好或者不如React好。没有它们，React就不能工作。然而，在更大的Web应用中直接使用DOM的确有一些痛点，通常这些痛点出现在变更检测方面。当数据变化时，我们希望通过更新UI来反映它，但很难以一种有效且易于理解的方式做到这点，所以React致力于解决这个问题。

出现这个问题的部分原因是浏览器处理与DOM交互的方式。当访问、修改或创建DOM元素时，浏览器常常要在一个结构化的树上执行查询来找到指定的元素。这只是访问一个元素，而且通常仅是更新的第一部分。通常情况下，作为更改的一部分，它不得不重新进行布局、缩放和其他操作——所有这些操作往往计算量都很大。虚拟DOM也无法绕过这个问题，但它可以在这些限制下帮助优化对DOM的更新。

当创建和管理一个处理随时间变化的数据的大型应用时，可能需要对DOM进行许多更改，这些更改通常会发生冲突或以不太理想的方式完成。这可能会导致一个过于复杂的系统，这个系统不但对工程师来说难以使用而且可能会导致用户体验不佳——这是“双输”。因此，性能是React设计和实现的另一个关键考虑因素。实现虚拟DOM有助于解决这个问题，但应该注意的是，它设计得只是“够快”而已。React的虚拟DOM更为重要的是提供了健壮的API、简单的思维模型和诸如跨浏览器兼容性等其他特性，而不是对性能的极端关注。我之所以强调这一点是因为人们可能听说虚拟DOM是某种“性能银弹”。它确实是高性能的，但它并不是神奇的“性能银弹”，最后我想说的是，React的许多其他好处对于使用React更为重要。

