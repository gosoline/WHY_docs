<!-- @format -->

```ini
# 编辑自 `yapf --style-help` 所生成的配置文件
# 参照 https://github.com/google/yapf#knobs 的谷歌翻译

[style]
# 将右括号与可视缩进对齐.
align_closing_bracket_with_visual_indent=True

# 允许字典键存在于多行中. 例如:
#
#   x = {
#       ('this is the first element of a tuple',
#        'this is the second element of a tuple'):
#            value,
#   }
allow_multiline_dictionary_keys=False

# 允许在多行上格式化 lambda 函数.
allow_multiline_lambdas=False

# 允许在参数列表中的默认/命名赋值之前拆分.
allow_split_before_default_or_named_assigns=True

# 允许在字典值之前拆分.
allow_split_before_dict_value=True

#   让间距指示运算符优先级. 例如:
#
#     a = 1 * 2 + 3 / 4
#     b = 1 / 2 - 3 * 4
#     c = (1 + 2) * (3 - 4)
#     d = (1 - 2) / (3 + 4)
#     e = 1 * 2 - 3
#     f = 1 + 2 + 3 + 4
#
# 将按如下格式设置以指示优先级:
#
#     a = 1*2 + 3/4
#     b = 1/2 - 3*4
#     c = (1+2) * (3-4)
#     d = (1-2) / (3+4)
#     e = 1*2 - 3
#     f = 1 + 2 + 3 + 4
#
arithmetic_precedence_indication=False

# 顶级函数和类定义周围的空行数
blank_lines_around_top_level_definition=2

# 顶级导入和变量定义之间的空行数.
blank_lines_between_top_level_imports_and_variables=1

# 在类级文档字符串之前插入一个空行.
blank_line_before_class_docstring=False

# 在模块文档字符串之前插入一个空行.
blank_line_before_module_docstring=False

# 在紧邻嵌套在另一个'def'或'class'中的'def'或'class'之前插入一个空行. 例如:
#
#   class Foo:
#                      # <------ 这个空行
#     def method():
#       ...
blank_line_before_nested_class_or_def=True

# 不要拆分连续的括号. 仅在设置 dedent_closing_brackets 时相关. 例如:
#
#    call_func_that_takes_a_dict(
#        {
#            'key1': 'value1',
#            'key2': 'value2',
#        }
#    )
#
# 将重新格式化为:
#
#    call_func_that_takes_a_dict({
#        'key1': 'value1',
#        'key2': 'value2',
#    })
coalesce_brackets=False

# 列限制.
column_limit=79

# 连续对齐的样式. 可能的值是:
#
# - SPACE: 使用空格连续对齐. 这是默认行为.
# - FIXED: 使用 (CONTINUATION_INDENT_WIDTH) 的固定列数
#          (即:CONTINUATION_INDENT_WIDTH/INDENT_WIDTH 个制表符
#          或 CONTINUATION_INDENT_WIDTH 个空格)连续对齐.
# - VALIGN-RIGHT: 将续行垂直对齐到多个 INDENT_WIDTH 列.
#          如果不能垂直对齐带有缩进字符的续行, 则略微向右
#          (一个制表符或几个空格).
continuation_align_style=SPACE

# 用于续行的缩进宽度.
continuation_indent_width=4

# 如果括号中的表达式不能放在一行中, 则将右括号放在单独的行上并少一级缩进.
# 适用于各种括号, 包括函数定义和调用. 例如:
#
#   config = {
#       'key1': 'value1',
#       'key2': 'value2',
#   }        # <--- 这个括号少一级缩进并且在一个单独的行上
#
#   time_series = self.remote_client.query_entity_counters(
#       entity='dev3246.region1',
#       key='dns.query_latency_tcp',
#       transform=Transformation.AVERAGE(window=timedelta(seconds=60)),
#       start_ts=now()-timedelta(days=3),
#       end_ts=now(),
#   )        # <--- 这个括号少一级缩进并且在一个单独的行上
dedent_closing_brackets=False

# 如果列表以逗号结尾, 则禁用将每个列表元素放在单独行上的启发式.
disable_ending_comma_heuristic=False

# 将每个词典条目放在自己的行上.
each_dict_entry_on_separate_line=True

# 需要多行字典, 即使它通常适合一行. 例如:
#
#   config = {
#       'key1': 'value1'
#   }
force_multiline_dict=False

# i18n 注释的正则表达式.
# 此注释的存在会停止对该行的重新格式化, 因为注释需要紧挨着它们翻译的字符串.
i18n_comment=

# i18n 函数调用名称.
# 此函数的存在会停止对该行的重新格式化, 因为它所具有的字符串无法从 i18n 注释中移走.
i18n_function_call=

# 缩进空行.
indent_blank_lines=False

# 如果括号中的表达式不能放在一行中, 则将右括号放在单独的行上并缩进.
# 适用于各种括号, 包括函数定义和调用. 例如:
#
#   config = {
#       'key1': 'value1',
#       'key2': 'value2',
#       }        # <--- 这个括号是缩进的并且在单独的一行上
#
#   time_series = self.remote_client.query_entity_counters(
#       entity='dev3246.region1',
#       key='dns.query_latency_tcp',
#       transform=Transformation.AVERAGE(window=timedelta(seconds=60)),
#       start_ts=now()-timedelta(days=3),
#       end_ts=now(),
#       )        # <--- 这个括号是缩进的并且在单独的一行上
indent_closing_brackets=False

# 如果字典值不能与字典键放在同一行, 则缩进字典值. 例如:
#
#   config = {
#       'key1':
#           'value1',
#       'key2': value1 +
#               value2,
#   }
indent_dictionary_value=False

# 用于缩进的列数.
indent_width=4

# 将短行合并为一行. 例如, 单行'if'语句.
join_multiple_lines=True

# 不要在选定的二元运算符周围包含空格. 例如:
#
#   1 + 2 * 3 - 4 / 5
#
# 配置为 "*,/" 时会格式化如下:
#
#   1 + 2*3 - 4/5
no_spaces_around_selected_binary_operators=

# 在默认或命名分配周围使用空格.
spaces_around_default_or_named_assign=False

# 在字典定界符的'{'之后和'}'之前添加一个空格.
#
#   {1: 2}
#
# 将被格式化为:
#
#   { 1: 2 }
spaces_around_dict_delimiters=False

# 在列表分隔符的'['之后和']'之前添加一个空格.
#
#   [1, 2]
#
# 将被格式化为:
#
#   [ 1, 2 ]
spaces_around_list_delimiters=False

# 在幂运算符周围使用空格.
spaces_around_power_operator=False

# 在下标/切片运算符周围使用空格. 例如:
#
#   my_list[1 : 10 : 2]
spaces_around_subscript_colon=False

# 在元组定界符的'('之后和')'之前添加一个空格.
#
#   (1, 2, 3)
#
# 将被格式化为:
#
#   ( 1, 2, 3 )
spaces_around_tuple_delimiters=False

# 结尾注释前所需的空格数.
# 这可以是一个单一的值(代表每个尾部注释之前的空格数),
# 也可以是值的列表(代表对齐列的值;
# 在一个块中的尾部注释将对齐到第一个大于块内最大行长度的列值).
# 例如:
#
# 当 spaces_before_comment=5:
#
#   1 + 1 # Adding values
#
# 将被格式化为:
#
#   1 + 1     # Adding values <-- 末尾之间有 5 个空格
#             # statement and comment
#
# 当 spaces_before_comment=15, 20:
#
#   1 + 1 # Adding values
#   two + two # More adding
#
#   longer_statement # This is a longer statement
#   short # This is a shorter statement
#
#   a_very_long_statement_that_extends_beyond_the_final_column # Comment
#   short # This is a shorter statement
#
# 将被格式化为:
#
#   1 + 1          # Adding values <-- 块中的行尾注释
#                  # 对齐到第15列
#   two + two      # More adding
#
#   longer_statement    # This is a longer statement <-- 行结束
#                       # 块中的注释对齐到第20列
#   short               # This is a shorter statement
#
#   a_very_long_statement_that_extends_beyond_the_final_column  # Comment <-- 行尾注释根据行长对齐
#   short                                                       # This is a shorter statement
#
spaces_before_comment=2

# 在列表之类的结尾逗号和右括号之间插入一个空格.
space_between_ending_comma_and_closing_bracket=True

# 在方括号、花括号和圆括号内使用空格. 例如:
#
#   method_call( 1 )
#   my_dict[ 3 ][ 1 ][ get_index( *args, **kwargs ) ]
#   my_set = { 1, 2, 3 }
space_inside_brackets=False

# 在参数之前拆分
split_all_comma_separated_values=False

# 在参数之前拆分, 但不要递归拆分所有子表达式(除非需要).
split_all_top_level_comma_separated_values=False

# 如果参数列表以逗号终止, 则在参数之前拆分.
split_arguments_when_comma_terminated=False

# 设置为 True 以优先在'+'、'-'、'*'、'/'、'//'或'@'之前拆分.
split_before_arithmetic_operator=False

# 设置为 True 以优先在 '&'、'|'  或 '^' 之前拆分.
split_before_bitwise_operator=True

# 如果列表或字典文字不适合单行, 则在右括号之前拆分.
split_before_closing_bracket=True

# 在字典或集合生成器 (comp_for) 之前拆分.
# 例如, 注意'for'之前的拆分:
#
#   foo = {
#       variable: 'Hello world, have a nice day!'
#       for variable in bar if variable != 42
#   }
split_before_dict_set_generator=True

# 在 '.' 之前拆分 如果我们需要拆分一个较长的表达式:
#
#   foo = ('This is a really long string: {}, {}, {}, {}'.format(a, b, c, d))
#
# 会重新格式化成类似的东西:
#
#   foo = ('This is a really long string: {}, {}, {}, {}'
#          .format(a, b, c, d))
split_before_dot=False

# 如果表达式不适合单行, 则在围绕表达式的左括号之后拆分.
split_before_expression_after_opening_paren=False

# 如果要拆分参数/参数列表, 则在第一个参数之前拆分.
split_before_first_argument=False

# 设置为 True 以优先在'and'或'or'之前而不是之后拆分.
split_before_logical_operator=True

# 将命名分配拆分到单独的行中.
split_before_named_assigns=True

# 设置为 True 以拆分列表推导式和生成器, 这些推导式和生成器在每个子句之前具有非平凡表达式和多个子句. 例如:
#
#   result = [
#       a_long_var + 100 for a_long_var in xrange(1000)
#       if a_long_var % 10]
#
# 会重新格式化成类似的东西:
#
#   result = [
#       a_long_var + 100
#       for a_long_var in xrange(1000)
#       if a_long_var % 10]
split_complex_comprehension=False

# 在开括号后立即分裂的惩罚.
split_penalty_after_opening_bracket=300

# 在一元运算符之后拆分行的惩罚.
split_penalty_after_unary_operator=10000

# 在'+'、'-'、'*'、'/'、'//'、'%'和'@'运算符周围拆分行的惩罚.
split_penalty_arithmetic_operator=300

# 在 if 表达式之前拆分的惩罚.
split_penalty_before_if_expr=0

# 在'&'、'|'和'^'运算符周围拆分行的惩罚.
split_penalty_bitwise_operator=300

# 拆分列表理解或生成器表达式的惩罚.
split_penalty_comprehension=80

# 字符超过列限制的惩罚.
split_penalty_excess_character=7000

# 通过向逻辑行添加行拆分而招致的惩罚. 添加的线分割越多, 惩罚越高.
split_penalty_for_added_line_split=30

# 拆分'import as'名称列表的惩罚. 例如:
#
#   from a_very_long_or_indented_module_name_yada_yad import (long_argument_1,
#                                                             long_argument_2,
#                                                             long_argument_3)
#
# 会重新格式化成类似的东西:
#
#   from a_very_long_or_indented_module_name_yada_yad import (
#       long_argument_1, long_argument_2, long_argument_3)
split_penalty_import_names=0

# 在'and'和'or'运算符周围拆分行的惩罚.
split_penalty_logical_operator=300

# 使用 Tab 字符缩进.
use_tabs=False
```
