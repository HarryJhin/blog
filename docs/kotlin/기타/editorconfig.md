---
title: Kotlin을 위한 editorconfig 구성
comments: true
---

[editorconfig 더 알아보기](https://www.jetbrains.com/help/idea/editorconfig.html){ target="_blank" .md-button .md-button--primary }

``` md
root = true

[*]
charset = utf-8
end_of_line = lf
indent_size = 4
indent_style = space
insert_final_newline = true
max_line_length = 120
tab_width = 4
ij_continuation_indent_size = 4
ij_smart_tabs = false
ij_visual_guides = none
ij_wrap_on_typing = true

[{**/*.kt,**/*.kts}]
# ktlint only [FIX]
disabled_rules = import-ordering
ktlint_code_style = official

# ---------------------------------------------------------------------------------------------------- #

# 탭 및 들여쓰기 [FIX]
ij_kotlin_keep_indents_on_empty_lines = false # 빈 줄에 주변 코드 줄과 동일한 들여쓰기가 적용되어 있는지 확인합니다

# ---------------------------------------------------------------------------------------------------- #

# 공백 > 소괄호 앞 [FIX]
ij_kotlin_space_before_if_parentheses = true # if
ij_kotlin_space_before_for_parentheses = true # for
ij_kotlin_space_before_while_parentheses = true # while
ij_kotlin_space_before_catch_parentheses = true # catch
ij_kotlin_space_before_when_parentheses = true # when

# 공백 > 연산자 주변 [FIX]
ij_kotlin_spaces_around_assignment_operators = true # 대입 연산자(=, +=, ...)
ij_kotlin_spaces_around_logical_operators = true # 논리 연산자(&&, ||)
ij_kotlin_spaces_around_equality_operators = true # 상등 연산자(==, !=)
ij_kotlin_spaces_around_relational_operators = true # 비교 연산자(<, >, <=, >=)
ij_kotlin_spaces_around_additive_operators = true # 덧셈 연산자(+, -)
ij_kotlin_spaces_around_multiplicative_operators = true # 곱셈 연산자(*, /, %)
ij_kotlin_spaces_around_unary_operator = false # 단항 연산자(!, -, +, ++, --)
ij_kotlin_spaces_around_range = false # 범위 연산자(.., ..<)

# 공백 > 기타 [FIX]
ij_kotlin_space_before_comma = false # 쉼표 앞
ij_kotlin_space_after_comma = true # 쉼표 뒤에
ij_kotlin_space_before_type_colon = false # 콜론 앞, 타입 선언 뒤
ij_kotlin_space_after_type_colon = true # 콜론 뒤, 타입 선언 앞
ij_kotlin_space_before_extend_colon = true # 새 타입 정의 내 콜론 앞
ij_kotlin_space_after_extend_colon = true # 새 타입 정의 내 콜론 뒤
ij_kotlin_insert_whitespaces_in_simple_one_line_method = true # 간단한 한 줄 메서드로
ij_kotlin_spaces_around_function_type_arrow = true # 함수 타입의 화살표 주위
ij_kotlin_spaces_around_when_arrow = true # "when" 절의 화살표 주위
ij_kotlin_space_before_lambda_arrow = true # 람다 화살표 앞

# ---------------------------------------------------------------------------------------------------- #
# ij_kotlin_wrap_elvis_expressions = 1 #
# ij_kotlin_wrap_expression_body_functions = 1 #
# ij_kotlin_align_in_columns_case_branch = false #
# ij_kotlin_allow_trailing_comma_on_call_site = false #

# 줄 바꿈 및 괄호 > 서식 다시 지정 시 유지
ij_kotlin_keep_line_breaks = true # 서식 지정 도구 또는 최종 사용자가 줄 바꿈을 추가했는지 여부에 관계없이 코드에 이미 적용된 줄 바꿈을 유지합니다
ij_kotlin_keep_first_column_comment = false # 첫 번째 열에서 시작하는 주석을 들여쓰기 하지 않은 상태로 둡니다

# 줄 바꿈 및 괄호 > extends/implements/permits 목록
# ij_kotlin_extends_list_wrap = normal
# ij_kotlin_align_multiline_extends_list = false # 여러 줄일 경우 정렬
# ij_kotlin_continuation_indent_in_supertype_lists = false # 연속 들여쓰기 허용

# 줄 바꿈 및 괄호 > 함수 선언 매개변수
# ij_kotlin_method_parameters_wrap = on_every_item # 정렬
# ij_kotlin_align_multiline_parameters = false # 여러 줄일 경우 정렬
# ij_kotlin_method_parameters_new_line_after_left_paren = true # `(` 뒤에 새 줄
# ij_kotlin_method_parameters_right_paren_on_new_line = true # `)` 뒤에 새 줄
# ij_kotlin_continuation_indent_in_argument_lists = false # 연속 들여쓰기 사용

# 줄 바꿈 및 괄호 > 함수 호출 인수
# ij_kotlin_call_parameters_wrap = on_every_item # 정렬
# ij_kotlin_align_multiline_parameters_in_calls = false # 여러 줄일 경우 정렬
# ij_kotlin_call_parameters_new_line_after_left_paren = true # `(` 뒤에 새 줄
# ij_kotlin_call_parameters_right_paren_on_new_line = true # `)` 뒤에 새 줄
# ij_kotlin_continuation_indent_in_parameter_lists = false # 연속 들여쓰기 사용

# 줄 바꿈 및 괄호 > 함수 소괄호
# ij_kotlin_align_multiline_method_parentheses = false # 여러 줄일 경우 정렬

# 줄 바꿈 및 괄호 > 체인 함수 호출
# ij_kotlin_method_call_chain_wrap = off
# ij_kotlin_wrap_first_method_in_call_chain = false # 첫 번쨰 호출 줄 바꿈
# ij_kotlin_continuation_indent_for_chained_calls = true # 연속 들여쓰기 사용

# 줄 바꿈 및 괄호 > `if()`문
# ij_kotlin_else_on_new_line = false # 새 줄에 `else`
# ij_kotlin_if_rparen_on_new_line = false # 새 줄에 `)` 배치
# ij_kotlin_continuation_indent_in_if_conditions = false # 조건에서 연속 들여쓰기 사용

# 줄 바꿈 및 괄호 > `do ... while()`문
ij_kotlin_while_on_new_line = false # 새 줄에 `while`

# 줄 바꿈 및 괄호 > `try`문
ij_kotlin_catch_on_new_line = false # 새 줄에 `catch`
ij_kotlin_finally_on_new_line = false # 새 줄에 `finally`

# 줄 바꿈 및 괄호 > 이진 표현식
# ij_kotlin_align_multiline_binary_operation = false # 여러 줄일 경우 정렬

# 줄 바꿈 및 괄호
# ij_kotlin_assignment_wrap = on_every_item # 대입 구문
# ij_kotlin_enum_constants_wrap = on_every_item # 열거형 상수
# ij_kotlin_class_annotation_wrap = on_every_item # 클래스 어노테이션
# ij_kotlin_method_annotation_wrap = off # 함수 어노테이션
# ij_kotlin_variable_annotation_wrap = split_into_lines # 프로퍼티 어노테이션
# ij_kotlin_parameter_annotation_wrap = off # 매개변수 어노테이션
# ij_kotlin_field_annotation_wrap = split_into_lines # 지역 변수 어노테이션

# `when` 구문
# ij_kotlin_line_break_after_multiline_when_entry = true # 여러 줄의 입력 이후 새로운 줄

# 중괄호 배치
# ij_kotlin_lbrace_on_next_line = false # 새 줄에 왼쪽 중괄호 배치

# 표현식 본문 함수
# ij_kotlin_continuation_indent_for_expression_bodies = false # 연속 들여쓰기 사용

# Elvis 식
# ij_kotlin_continuation_indent_in_elvis = false # 연속 들여쓰기 사용

# ---------------------------------------------------------------------------------------------------- #

# # 빈 줄 > 최대 빈 줄 유지 [FIX]
ij_kotlin_keep_blank_lines_in_declarations = 1 # 선언 내
ij_kotlin_keep_blank_lines_in_code = 1 # 코드 내
ij_kotlin_keep_blank_lines_before_right_brace = 1 # `}` 앞

# 빈 줄 > 최소 빈 줄 [FIX]
ij_kotlin_blank_lines_after_class_header = 0 # 클래스 헤더 뒤
ij_kotlin_blank_lines_around_block_when_branches = 0 # `{}`가 있는 `when` 브랜치 주위
ij_kotlin_blank_lines_before_declaration_with_comment_or_annotation_on_separate_line = 1 # 주석 또는 어노테이션이 있는 선언 앞

# ---------------------------------------------------------------------------------------------------- #

# 가져오기 > 최상위 심볼 [FIX]
ij_kotlin_name_count_to_use_star_import = 2147483647 # 단일 이름 import 문 사용

# 가져오기 > Java static 및 열거형 멤버 [FIX]
ij_kotlin_name_count_to_use_star_import_for_members = 2147483647 # 단일 이름 import 사용

# 가져오기 > 기타 [FIX]
ij_kotlin_import_nested_classes = false # 중첩된 클래스에 대한 import 문 삽입

# 가져오기 > `*`가 포함된 import 문을 사용하는 패키지 [FIX]
ij_kotlin_packages_to_use_import_on_demand = unset

# 가져오기 > 레이아웃 가져오기 [FIX]
ij_kotlin_imports_layout = *, java.**, javax.**, kotlin.**, ^

# ---------------------------------------------------------------------------------------------------- #

# 기타
# ij_kotlin_allow_trailing_comma = false # 후행 쉼표 사용

# ---------------------------------------------------------------------------------------------------- #

# 코드 생성 [FIX]
ij_kotlin_line_comment_at_first_column = false # 첫 번쨰 열의 줄 주석
ij_kotlin_line_comment_add_space = true # 줄 주석 시작 부분에 공백 추가
ij_kotlin_line_comment_add_space_on_reformat = true # 서식 다시 지정 시 강제 적용
ij_kotlin_block_comment_at_first_column = true # 첫 번쨰 열의 블록 주석
ij_kotlin_block_comment_add_space = false # 블록 주석 주변에 공백 추가

# ---------------------------------------------------------------------------------------------------- #

# 로드/저장 [FIX]
ij_kotlin_code_style_defaults = KOTLIN_OFFICIAL
```
