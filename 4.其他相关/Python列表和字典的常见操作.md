```python
# ========== 列表操作 ==========

# 创建列表
fruits = ['apple', 'banana', 'orange', 'grape', 'kiwi']
numbers = [1, 3, 5, 2, 8, 4, 6]

# 访问元素
print("第一个水果:", fruits[0])
print("最后一个水果:", fruits[-1])
print("前三个水果:", fruits[:3])

# 添加元素
fruits.append('mango')  # 末尾添加
fruits.insert(1, 'pear')  # 指定位置插入
print("添加元素后:", fruits)

# 删除元素
removed_fruit = fruits.pop()  # 删除并返回最后一个元素
fruits.remove('banana')  # 删除特定元素
print("删除元素后:", fruits)

# 排序
fruits.sort()  # 原地排序
print("排序后的水果:", fruits)

numbers_sorted = sorted(numbers)  # 返回新排序列表
print("原始数字:", numbers)
print("排序后的数字:", numbers_sorted)

# 列表推导式
squared_numbers = [x**2 for x in numbers]
print("数字的平方:", squared_numbers)

even_numbers = [x for x in numbers if x % 2 == 0]
print("偶数:", even_numbers)

# 列表长度
print("水果数量:", len(fruits))

# ========== 字典操作 ==========

# 创建字典
person = {
    'name': 'Alice',
    'age': 30,
    'city': 'New York',
    'occupation': 'Engineer'
}

# 访问值
print("姓名:", person['name'])
print("年龄:", person.get('age'))
print("不存在的键:", person.get('country', '未知'))

# 添加/修改键值对
person['email'] = 'alice@example.com'  # 添加新键
person['age'] = 31  # 修改现有键

# 删除键值对
removed_value = person.pop('occupation')  # 删除并返回
print("删除的职业:", removed_value)

# 遍历字典
print("\n遍历键:")
for key in person:
    print(key)

print("\n遍历键值对:")
for key, value in person.items():
    print(f"{key}: {value}")

# 字典推导式
squared_dict = {x: x**2 for x in range(1, 6)}
print("平方字典:", squared_dict)

# 合并字典
additional_info = {'hobby': 'reading', 'nationality': 'American'}
person.update(additional_info)
print("合并后的个人信息:", person)

# ========== 嵌套结构 ==========

# 列表嵌套字典
students = [
    {'name': 'Bob', 'grade': 85},
    {'name': 'Charlie', 'grade': 92},
    {'name': 'Diana', 'grade': 78}
]

# 按成绩排序
students_sorted = sorted(students, key=lambda x: x['grade'], reverse=True)
print("\n按成绩排序的学生:")
for student in students_sorted:
    print(f"{student['name']}: {student['grade']}")

# 字典嵌套列表
classroom = {
    'teacher': 'Mr. Smith',
    'students': ['Emma', 'Frank', 'Grace', 'Henry'],
    'subjects': ['Math', 'Science', 'History']
}

print("\n教室信息:")
print(f"老师: {classroom['teacher']}")
print(f"学生数量: {len(classroom['students'])}")
print(f"科目: {', '.join(classroom['subjects'])}")

# 复杂结构：字典嵌套字典
school = {
    'class1': {
        'teacher': 'Mrs. Johnson',
        'students': 25,
        'average_grade': 87.5
    },
    'class2': {
        'teacher': 'Mr. Davis',
        'students': 22,
        'average_grade': 91.2
    }
}

print("\n学校信息:")
for class_name, class_info in school.items():
    print(f"{class_name}: {class_info['teacher']} 老师, "
          f"{class_info['students']} 名学生, "
          f"平均成绩 {class_info['average_grade']}")

# ========== 其他实用操作 ==========

# 使用zip函数组合列表
names = ['Alice', 'Bob', 'Charlie']
scores = [95, 87, 91]
name_score_pairs = list(zip(names, scores))
print("\n姓名-分数对:", name_score_pairs)

# 使用enumerate获取索引和值
print("\n带索引的水果列表:")
for index, fruit in enumerate(fruits):
    print(f"{index}: {fruit}")

# 过滤列表
high_scores = [score for score in scores if score >= 90]
print("高分:", high_scores)

# 字典键值反转
original_dict = {'a': 1, 'b': 2, 'c': 3}
reversed_dict = {v: k for k, v in original_dict.items()}
print("反转后的字典:", reversed_dict)
```