# mass_edit
Mass Edit V11

1. fix NameError: name 'basestring' is not defined at python 3.x by laoliu
2. fix ValueError: Invalid domain term ('model_id', 'in', <map object at 0x7fdf55d2bef0>) by laoliu
3. fix _inherits model,ValueError: Invalid domain term ('model', 'in', dict_keys(['res.partner'])) by hui


* Nitice: change dir name to mass_editing

Ps：来自：http://www.jointd.com/?p=3563
Odoo第三方模块Mass edit更新至odoo11，name ‘basestring’ is not defined ，ValueError: Invalid domain term

Odoo第三方模块Mass edit更新至odoo11:name 'basestring' is not defined ，ValueError: Invalid domain term
fix name 'basestring' is not defined at python 3.x by laoliu，
fix _inherits model,ValueError: Invalid domain term ('model', 'in', dict_keys(['res.partner'])) ValueError: Invalid domain term ('model_id', 'in',
) by hui
有时候会需要批量编辑某个字段多条记录的值，
比如，批量把用户的时区设为上海，用户很多时，一个个改，还是很费时间的，
在有mass edit这个模块之前，可以通过系统自带的导出，然后修改，再导入来实现，
或者写个server action,
有了mass edit,这些就变得方便了，
不知为何，OCA迟迟没有把这个模块更新到v11, 而官网上那个v11的版本又会报错，
在石家庄老刘和我们工程师小张的努力下，修改了3个地方，模块又能用了。
我们把代码也放到了github上：https://github.com/zykj/mass_edit_v11
具体改了下面几个地方
目录名要修改为mass_edit,
mass_object.py中 unlink_action 方法需要注释掉一行（感谢-石家庄老刘），
            # see line 27
            #self.mapped('ref_ir_value_id').sudo().unlink()
PythonCopy
mass_object.py中增加一行,这样就能正确用在那些 _inherits 继承的对象上了，比如 res.user用户：
keys = list(keys) 
PythonCopy
xml 中的domain这里要修改下，这是因为python3.x map返回的是object,而2.7中map的返回的是列表，改为
                            domain="[('ttype', 'not in', ['reference', 'function']), ('model_id', '=', model_id)]"/>
XMLCopy
赞 0 赏 分享
 发表评论
 509 views
 
A+
发布日期：2018年07月20日  所属分类：Odoo OpenERP
标签：Invalid domain termmass editname 'basestring' is not definedodooodoo11
