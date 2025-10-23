highlight guidance:
* 重点关注定义、定理、公式、核心论点和老师强调的内容。
* 重点关注数据、证据、引用、不同观点和强有力的结论。
* 重点关注让读者感到惊讶、有启发或与已有知识产生连接的部分。

audience highlight adaptation guidance:
* 默认读者：如果未提供受众信息，默认按「高中/大学入门级」处理，避免选取过于抽象或强背景依赖的句子。
* 选择优先级（从高到低，面向学生/入门）：
  1) 基础概念/明确定义/关键术语的界定
  2) 具体可感知的例子、直观类比、可操作的步骤/流程
  3) 教学中老师强调的内容、阶段性小结、显式因果/条件关系
  4) 与已有知识建立连接的桥接句、学习建议/提醒常见误解
  5) 数据与证据（优先叙述清晰、直接支持观点的句子）
  6) 强推理或高抽象的核心论点/强结论（仅当语言清晰且对入门者可理解时）
* 降权/避选（对学生）：
  - 需要大量领域背景才能理解的推断、方法学细节、限定条件繁多的句子
  - 仅有修辞而缺乏信息量的感叹句
  - 未定义的新术语堆叠
* 术语与缺口：若选中的句子包含生僻术语或隐含前置知识，应在 gap 中标注「未知术语/所需先修」。
* 若同段落存在「概念定义」与「高抽象结论」同时出现，优先返回概念定义或具体例子。
* 同段落若存在可替代的更易懂表达（仍需逐字引用），优先选择语义完整、句式更直白的那一句。
* 若整段仅包含过度抽象/背景依赖信息，则允许不做高亮（results 对应项可省略，或返回空 result）。

highlight workflow:
for each paragraph |> pinpointing the most crucial sentences for emphasis and returning them as direct quotes. If the paragraph has no main point, then highlight can be empty.

final_output_spec:
The output should be a VALID YAML document with the following keys:
* 'schema_version':
  - Data Type: string
  - Description: 结果结构的版本号（语义化版本，便于向后兼容）
  - Constraints: format: semver
  - Required: false
* 'document_id':
  - Data Type: string
  - Description: 源文档唯一标识（例如 UUID 或可读 slug）
  - Constraints: assumed string; format: uuid or slug
  - Required: false
* 'language':
  - Data Type: string
  - Description: 文档语言代码（BCP 47，例如 en, zh-CN）
  - Constraints: format: bcp47
  - Required: false
* 'created_at':
  - Data Type: timestamp
  - Description: 结果生成时间（ISO 8601 日期时间）
  - Constraints: format: date-time (ISO 8601)
  - Required: false
* 'results':
  - Data Type: array
  - Description: “关键句”提取结果列表
  - Constraints: order must follow original paragraph order
  - Required: true
  - Items:
    - Description: “关键句”提取结果对象
    - Data Type: object
    - Required: true
    - Default for item: null
    - Element:
      * 'result' (within items):
        - Data Type: object
        - Description: “关键句”提取结果对象
        - Required: true
        - Properties:
          * 'rationale':
            - Description: 简要理由，说明为何该句关键（可选说明/审计用）
            - Data Type: string
            - Required: false
          * 'type':
            - Description: 引用的分类
            - Constraints: enum: ['基础概念', '关键术语', '举例', '类比', '常见误解', '学习建议', '步骤/流程', '图示/结构描述', '背景知识', '关键问题', '定义', '定理', '公式', '核心论点', '教学中老师强调的内容', '数据', '证据', '引用', '不同观点', '强有力的结论', '让读者感到惊讶', '有启发', '与已有知识产生连接', '<...其他, 按需求自动拓展生成>']
            - Data Type: string
            - Required: true
          * 'quotes':
            - Description: 被选中的“直接引用”句子(可以是多个句子, 可以是完整句子, 也可以是部分句子)，保持原文大小写与标点（不改写、不补充）
            - Constraints: verbatim from source; no paraphrasing; preserve punctuation and casing
            - Data Type: array<string>
            - Required: true
          * 'confidence':
            - Description: 选择为“关键句”的置信度
            - Constraints: minimum: 0.0; maximum: 1.0
            - Data Type: float
            - Required: true
          * 'gap':
            - Description: 标注影响置信度的信息缺口
            - Data Type: string
            - Required: true

final_output: .yaml