# OCLint  Shell  代码审查脚本
使用方法: 在工程所在目录下终端执行:
chmod +x /xxx/xxx/oclint.sh   
/xxx/xxx/oclint.sh 
即可,分析过程较慢,请耐心等待
# 更多规则请参阅https://github.com/oclint/oclint
脚本代码如下:

xcodebuild clean\
xcodebuild -workspace=grid  -scheme=grid | xcpretty -r json-compilation-database\
cp build/reports/compilation_db.json compile_commands.json\
oclint-json-compilation-database -e Pods -- \
-report-type html \
-rc=LONG_VARIABLE_NAME=20 \
-rc=ShortVariableName=4 \
-rc=LONG_CLASS=700 \
-rc=LONG_METHOD=80 \
-rc=LONG_LINE=200 \
-rc=NCSS_METHOD=120 \
-rc=NESTED_BLOCK_DEPTH=5 \
-rc=TOO_MANY_FIELDS=20 \
-rc=TOO_MANY_METHODS=30 \
-rc=TOO_MANY_PARAMETERS=6 \
-o=report.html
open ./report.html
# --命名
# 变量名字最长字节
#-rc=LONG_VARIABLE_NAME=20 /
# 变量名字最短字节
#-disable-rule ShortVariableName /
# --size
# 圈复杂度
#-re=CYCLOMATIC_COMPLEXITY=10 /
# 每个类最行数
#-rc=LONG_CLASS=700 /
# 每行字节数量
#-rc=LONG_LINE=200 /
# 每个方法行数
#-rc=LONG_METHOD=80 /
# 忽略注释后括号后的有效代码行数
#-rc=NCSS_METHOD=40 /
# 嵌套深度
#-rc=NESTED_BLOCK_DEPTH=5 /
# 字段数量
#-rc=TOO_MANY_FIELDS=20 /
# 方法数量
#-rc=TOO_MANY_METHODS=30 /
# 方法参数
#-rc=TOO_MANY_PARAMETERS=6

