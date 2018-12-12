
## 简介

- 在依赖高的系统中发布新版本包可能很快会成为噩梦。如果依赖关系过高，可能面临版本控制被锁死的风险（必须对每一个依赖包改版才能完成某次升级）。而如果依赖关系过于松散，又将无法避免版本的混乱（假设兼容于未来的多个版本已超出了合理数量）。当你专案的进展因为版本依赖被锁死或版本混乱变得不够简便和可靠，就意味着你正处于依赖地狱之中。

## 基本规则
版本格式：主版本号.次版本号.修订号，版本号递增规则如下：

    1. 主版本号：当你做了不兼容的 API 修改，
    2. 次版本号：当你做了向下兼容的功能性新增，
    3. 修订号：当你做了向下兼容的问题修正。

- 主版本号

1. 当主版本号等于0时（0.1.3）则认为当前版本为开发版本
2. 每次主版本号变更时则次版本号、修订号需要重置为0，如1.0.0
3. 1.0.0 版本则认为是开发版本与发布版本的界限
	
- 次版本号

	1. 当版本功能有新增或者大量的修改改正则递增
	2. 当API被启用、废弃时都需要递增
	
- 修订号

	1. 当对当前版本进行问题修复是递增
	
- 先行号

	1. 当在标准版本上开放新的验证类或者测试功能时新增
	2. 附加编译信息
	3. 在修订号后以“-”后追加，不允许有空格，只能是[0-9A-Za-z]

## 具体规范
1. 使用语义化版本控制的软件必须（MUST）定义公共 API。该 API 可以在代码中被定义或出现于严谨的文件内。无论何种形式都应该力求精确且完整。

2. 标准的版本号必须（MUST）采用 X.Y.Z 的格式，其中 X、Y 和 Z 为非负的整数，且禁止（MUST NOT）在数字前方补零。X 是主版本号、Y 是次版本号、而 Z 为修订号。每个元素必须（MUST）以数值来递增。例如：1.9.1 -> 1.10.0 -> 1.11.0。

3. 标记版本号的软件发行后，禁止（MUST NOT）改变该版本软件的内容。任何修改都必须（MUST）以新版本发行。

4. 主版本号为零（0.y.z）的软件处于开发初始阶段，一切都可能随时被改变。这样的公共 API 不应该被视为稳定版。

5. 1.0.0 的版本号用于界定公共 API 的形成。这一版本之后所有的版本号更新都基于公共 API 及其修改内容。

6. 修订号 Z（x.y.Z | x > 0）必须（MUST）在只做了向下兼容的修正时才递增。这里的修正指的是针对不正确结果而进行的内部修改。

7. 次版本号 Y（x.Y.z | x > 0）必须（MUST）在有向下兼容的新功能出现时递增。在任何公共 API 的功能被标记为弃用时也必须（MUST）递增。也可以（MAY）在内部程序有大量新功能或改进被加入时递增，其中可以（MAY）包括修订级别的改变。每当次版本号递增时，修订号必须（MUST）归零。

8. 主版本号 X（X.y.z | X > 0）必须（MUST）在有任何不兼容的修改被加入公共 API 时递增。其中可以（MAY）包括次版本号及修订级别的改变。每当主版本号递增时，次版本号和修订号必须（MUST）归零。

## 使用语义化版本号的好处
- 也即原规范中对为何要使用语义化版本号的描述。在我看来，无非就是在遵循了本规范后，透过版本号，你可以非常清楚地了解到你手头拿到的软件版本相比于上一个版本发生了怎样的变化，所以你在使用的时候可以更注意一下这些变化，以免出现不兼容的情况。

- 比如如果主版本号升级了，可以知道软件新增了功能且该功能或者重大问题修复，且都是与旧版本不兼容的。同时主版本号的更新也可以表明是次版本号更新到了一定程序，比如新增功能数量达到了一定指标，我们可以认为可以升级一下主版本号了。

- 如果次版本更新了，我们可以知道有小部分新功能添加，或者修订号更新，有小部分bug被修复，而在获取这些信息时完全还没有查看change log。这正是语义化的好处，版本号就告诉你大部分信息了。

- 另外个好处就是当大家都在遵循一个规范的时候，无疑扫清了一些认知上的障碍，将事情简单化，大家也心照不宣地能看懂每个人代码中的版本号的意思，初学者也很容易掌握这方面的知识。


## 常见问题及解答
- 在 0.y.z 初始开发阶段，我该如何进行版本控制？

    最简单的做法是以 0.1.0 作为你的初始化开发版本，并在后续的每次发行时递增次版本号。

- 如何判断发布 1.0.0 版本的时机？

    当你的软件被用于正式环境，它应该已经达到了 1.0.0 版。如果你已经有个稳定的 API 被使用者依赖，也会是 1.0.0 版。如果你很担心向下兼容的问题，也应该算是 1.0.0 版了。

- 这不会阻碍快速开发和迭代吗？

    主版本号为零的时候就是为了做快速开发。如果你每天都在改变 API，那么你应该仍在主版本号为零的阶段（0.y.z），或是正在下个主版本的独立开发分支中。

- 对于公共 API，若即使是最小但不向下兼容的改变都需要产生新的主版本号，岂不是很快就达到 42.0.0 版？

    这是开发的责任感和前瞻性的问题。不兼容的改变不应该轻易被加入到有许多依赖代码的软件中。升级所付出的代价可能是巨大的。要递增主版本号来发行不兼容的改版，意味着你必须为这些改变所带来的影响深思熟虑，并且评估所涉及的成本及效益比。

- 为整个公共 API 写文件太费事了！

    为供他人使用的软件编写适当的文件，是你作为一名专业开发者应尽的职责。保持专案高效一个非常重要的部份是掌控软件的复杂度，如果没有人知道如何使用你的软件或不知道哪些函数的调用是可靠的，要掌控复杂度会是困难的。长远来看，使用语义化版本控制以及对于公共 API 有良好规范的坚持，可以让每个人及每件事都运行顺畅。

- 万一不小心把一个不兼容的改版当成了次版本号发行了该怎么办？

    一旦发现自己破坏了语义化版本控制的规范，就要修正这个问题，并发行一个新的次版本号来更正这个问题并且恢复向下兼容。即使是这种情况，也不能去修改已发行的版本。可以的话，将有问题的版本号记录到文件中，告诉使用者问题所在，让他们能够意识到这是有问题的版本。

- 如果我更新了自己的依赖但没有改变公共 API 该怎么办？

    由于没有影响到公共 API，这可以被认定是兼容的。若某个软件和你的包有共同依赖，则它会有自己的依赖规范，作者也会告知可能的冲突。要判断改版是属于修订等级或是次版等级，是依据你更新的依赖关系是为了修复问题或是加入新功能。对于后者，我经常会预期伴随着更多的代码，这显然会是一个次版本号级别的递增。

- 如果我变更了公共 API 但无意中未遵循版本号的改动怎么办呢？（意即在修订等级的发布中，误将重大且不兼容的改变加到代码之中）

    自行做最佳的判断。如果你有庞大的使用者群在依照公共 API 的意图而变更行为后会大受影响，那么最好做一次主版本的发布，即使严格来说这个修复仅是修订等级的发布。记住， 语义化的版本控制就是透过版本号的改变来传达意义。若这些改变对你的使用者是重要的，那就透过版本号来向他们说明。

- 我该如何处理即将弃用的功能？

    弃用现存的功能是软件开发中的家常便饭，也通常是向前发展所必须的。当你弃用部份公共 API 时，你应该做两件事：
    
    （1）更新你的文件让使用者知道这个改变，
    
    （2）在适当的时机将弃用的功能透过新的次版本号发布。
    
    在新的主版本完全移除弃用功能前，至少要有一个次版本包含这个弃用信息，这样使用者才能平顺地转移到新版 API。

- 语义化版本对于版本的字串长度是否有限制呢？

    没有，请自行做适当的判断。举例来说，长到 255 个字元的版本已过度夸张。再者，特定的系统对于字串长度可能会有他们自己的限制。