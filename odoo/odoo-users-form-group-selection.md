### 如何把自定的组加入到用户界面中的Application ###
文件： res_users.py  
源码:
<pre>
def fields_get(self, cr, uid, allfields=None, context=None, write_access=True, attributes=None):
（省略）
        for app, kind, gs in self.pool['res.groups'].get_groups_by_application(cr, SUPERUSER_ID, context):
            if kind == 'selection':
                # selection group field
                tips = ['%s: %s' % (g.name, g.comment) for g in gs if g.comment]
                res[name_selection_groups(map(int, gs))] = {
                    'type': 'selection',
                    'string': app and app.name or _('Other'),
                    'selection': [(False, '')] + [(g.id, g.name) for g in gs],
                    'help': '\n'.join(tips),
                    'exportable': False,
                    'selectable': False,
                }

    def get_groups_by_application(self, cr, uid, context=None):
（省略）
        def linearized(gs):
            gs = set(gs)
            # determine sequence order: a group should appear after its implied groups
            order = dict.fromkeys(gs, 0)
            for g in gs:
                for h in gs.intersection(g.trans_implied_ids):
                    order[h] -= 1
            # check whether order is total, i.e., sequence orders are distinct
            if len(set(order.itervalues())) == len(gs):
                return sorted(gs, key=lambda g: order[g])
            return None
（省略）
        for app in apps:
            gs = linearized(by_app[app])
            if gs:
                res.append((app, 'selection', gs))
            else:
                res.append((app, 'boolean', by_app[app]))
</pre>  

如上代码的意思：
只有：len(set(order.itervalues())) == len(gs): 
kind 才会是 selection，才会加入到application中进行选择。  
就是指：
当前模块中的 组 相互不同层次的继承，  
如： A>B>C
则len(gs) = 3，set(order.itervalues()) = set([0,-1,-2])