# Agent 协作约定

## 适用范围
本约定作为仓库内 Halo2 主题工作的持久化记忆，默认长期生效。

## 项目基线
1. 项目为 Halo 2 主题 `theme-stellar`，由 Hexo 主题 Stellar 移植而来。
2. 当前主题版本为 `1.1.1`，要求 Halo 版本为 `>=2.22.1`，以 `theme.yaml` 中的实际值为准。
3. 主题展示名为 Stellar，主题许可证为 MIT License。
4. 项目以主题模板、配置和静态资源为主，不是独立的 Halo 后端插件。
5. 本节记录的是分析时基线；版本、依赖或目录发生变化时，应与实际代码同步更新。

## 协作规则
1. 实施前需报告关键官方来源（链接 + 核验日期）。
2. 文档存在歧义时，先澄清歧义再继续实现。
3. 需求变化后，及时更新本文件，保持约定与当前实践一致。
4. 完成本次项目基线分析后，后续任务默认直接按本文件和用户当次需求执行，不重复进行全仓分析。
5. 后续实施仍需完成与当次改动直接相关的定位、影响检查和验证，不得以“不再分析”为由跳过必要的工程检查。

## 语言约定
1. 新增或修改的自有注释、文档、页内标签与标题、面向用户的提示信息统一使用中文。
2. 第三方库原文、协议字段、API 必需字面量、框架保留键和现有英文国际化资源可保留英文，并在必要时于附近提供中文说明。
3. 分析文档、配置说明和交付报告中的字段展示统一使用 `字段（字段释义）` 形式。
4. 不强制将 YAML 键、代码变量、协议字段或正常界面文案改写为 `字段（字段释义）` 形式。

## 国际化要求
1. 国际化资源位于 `i18n/`，当前包含 `default.properties`、`zh.properties` 和 `en.properties`。
2. `default.properties` 与 `zh.properties` 默认使用中文，`en.properties` 保留英文翻译。
3. 新增或删除国际化键时，必须同步检查三个资源文件，保持键集一致。
4. 模板中可复用的界面文案应优先使用 Thymeleaf 消息表达式，避免在多个模板内重复硬编码。
5. 修改现有英文资源时，应保留其国际化用途，不得因“自有文案使用中文”而将英文翻译整体替换为中文。

## 技术栈与目录职责
1. 模板引擎：Halo 2 主题使用的 Thymeleaf，模板中使用 `th:*`、Finder 和 Halo 提供的模板上下文。
2. 前端实现：原生 HTML、CSS 和 JavaScript，仓库当前没有 Node.js 包管理或前端构建链声明。
3. 配置定义：YAML，包括主题元数据、主题设置和内容注解设置。
4. 项目工具：Gradle Wrapper 7.4，`build.gradle` 声明 Java 插件与 Thymeleaf `3.0.12.RELEASE` 依赖。
5. `templates/`：页面入口模板、可复用模块和主题静态资源。
6. `templates/modules/`：整体布局、页头页脚、变量、插件加载器、侧边栏、文章组件、评论与小工具等复用片段。
7. `templates/assets/`：主题自有 CSS、JavaScript、图片与随主题发布的第三方前端库。
8. `i18n/`：主题国际化消息资源。
9. `gradle/`、`gradlew` 与 `gradlew.bat`：Gradle Wrapper 及其启动脚本。
10. `docs/`：后续正式的约束性文档和输出性文档承载目录；可根据文档类型创建相应子目录或文件。

## 页面和模板映射
1. `index.html`：站点首页和文章列表入口。
2. `post.html`：默认文章详情页；`topic.html`：主题元数据中注册的“专题模板”。
3. `page.html`：默认独立页；`category_topic.html`：主题元数据中注册的“专题分类模板”。
4. `category.html` 与 `categories.html`：单分类和分类汇总页。
5. `tag.html` 与 `tags.html`：单标签和标签汇总页。
6. `archives.html`：归档页；`author.html`：作者相关页面。
7. `docs.html`、`doc.html` 与 `templates/modules/doc_layout.html`：文档系统列表、文档内容和文档专用布局。
8. `links.html`：友情链接页；`moments.html`：瞬间页；`photos.html`：图库页。
9. `douban.html`：豆瓣内容页，使用 `plugin-douban` 插件片段。
10. `equipments.html`：装备页，使用 `equipment` 插件片段。
11. `templates/error/404.html`：404 错误页。

## 文件职责
1. `theme.yaml`（主题元数据）：定义主题名称、版本、Halo 版本要求、作者、许可证、设置名称、ConfigMap 名称和自定义模板。
2. `settings.yaml`（主题设置入口）：定义 Halo 后台中的主题配置表单。当前分组包括 logo、侧边栏导航、站点主结构树、样式、评论、友链页、页脚、文章、小工具、图库、默认图片、扩展插件、API 地址和扩展设置。
3. `annotation-setting.yaml`（内容注解入口）：定义文章与独立页的额外字段，包括文章类型、缩进、GitHub 仓库和许可协议等。
4. `templates/modules/layout.html`（主布局）：常规页面的总体 HTML 骨架与槽位组装入口。
5. `templates/modules/head.html`（页头）：页面头部元数据和资源引用。
6. `templates/modules/variables/`（模板变量）：统一整理根变量与样式相关变量。
7. `templates/modules/partial/`（局部组件）：包含侧边栏、导航、文章列表、文章详情、评论和前端脚本片段。
8. `templates/modules/widgets/`（小工具）：目录、标签云、最近文章、作者、友链、瞬间、GitHub 仓库等可配置小工具。
9. `templates/modules/plugins/`（前端插件加载）：管理 Swiper、Fancybox、图片懒加载、页面预加载和代码复制等前端能力的引入。
10. `templates/assets/css/main.css`（主样式源）与 `main.min.css`（压缩样式）：两者的改动和发布关系必须保持同步，不得只修改其中一份却未说明原因。
11. `templates/assets/js/main.js`（主脚本）：站点通用交互入口。
12. `templates/assets/js/services/`（数据服务）：微博、时间线、站点、Memos、GitHub 信息和友链等外部或扩展数据处理。
13. `templates/assets/js/search/`（搜索）：本地搜索与 Algolia 搜索的前端实现。
14. `templates/assets/libs/`（第三方库）：随主题分发的 jQuery、Swiper、Fancybox、LazyLoad、Marked、Flying Pages 和标签云脚本等。
15. `README.md`（项目说明）：面向主题使用者和贡献者的功能、插件支持、文档与贡献入口。
16. `build.gradle`、`settings.gradle` 与 Gradle Wrapper（工程工具）：当前仅提供基础 Java/Thymeleaf Gradle 工程配置，未发现专用的主题打包、前端编译或自动化测试任务。

## 已知风险与维护注意事项
1. 本地 Java 版本为 21，Gradle Wrapper 版本为 7.4；当前执行 Gradle 任务会因 `Unsupported class file major version 65` 失败。调整 Java 或 Gradle 版本前需根据官方兼容性矩阵评估影响。
2. 仓库未声明 CSS 预处理、压缩或其他前端构建流程；修改 `main.css` 时需先明确 `main.min.css` 的同步方式。
3. 主题依赖 Halo 提供的 Finder 和模板变量，已使用的 Finder 包括 `postFinder`、`categoryFinder`、`tagFinder`、`menuFinder`、`friendFinder` 和 `momentFinder`。Halo 版本升级时需核对对应接口。
4. 友链、瞬间、图库、评论、搜索、代码高亮、豆瓣和装备等能力可能依赖 Halo 插件。修改相关模板时需同时检查插件未安装、未启用或数据为空时的行为。
5. `douban.html` 和 `equipments.html` 直接引用插件模板片段，插件名称或片段路径变化会直接导致页面渲染异常。
6. `settings.yaml` 体积较大且配置组较多，新增或重命名配置项时，必须全局检索 `theme.config`、默认值、条件显示和相关文档。
7. 主题包含英文国际化资源和第三方库源文，不应为统一中文而盲目翻译第三方代码或破坏国际化功能。
8. `README.md` 的 TODO 仅记录“细节优化”，不能作为具体实施范围；实际改动以用户需求和约束性文档为准。
9. 当前未发现自动化测试或主题专用验证任务；模板改动应至少完成语法检查、关联引用检查，并在可用的 Halo 环境中进行页面渲染验证。
10. 执行修改时应保留用户已有改动，不得因格式化或整文件重写而覆盖无关内容。

## 文档同步约定
1. 文档分为“约束性文档”和“输出性文档”两类。
2. 约束性文档（如 `agents.md`、后续在 `docs/` 中创建的产品定义、技术规范及其他规则或约束文件）定义实现边界，必须遵守，不以代码反向覆盖约束。
3. 若代码实现超出约束性文档范围，必须单独提供“偏差表”，至少包含：偏差项、偏差原因、影响与风险、回退或修正方案。
4. 输出性文档（如说明书、汇总文件、验证记录等）必须与代码和运行事实一致，发现不一致时应按事实及时同步。
5. 文档核查与同步属于交付步骤的一部分，默认与代码改动同批完成，不延后。
6. `docs/` 目录或其中具体文档尚未创建时，仅表示预留的文档承载位置，不得将尚不存在的文档视为已生效的约束。
