# 调整tree的列宽 #
参考链接
[http://107.167.187.43/index.php/topics/view/view-column-widths](http://107.167.187.43/index.php/topics/view/view-column-widths)
1：增加css
<pre>
.trans_attribute th[data-id='attribute_id'] {
  width: 20%;
}
</pre>
2：加载CSS

    <template id="assets_backend" name="Product Manage assets" inherit_id="web.assets_backend">
        <xpath expr="." position="inside">
            <link rel="stylesheet" href="/batar_internal_trans/static/src/css/attribute.css"/>
        </xpath>
    </template>
3：tree中加入class

    <tree editable="buttom" create="1" class="trans_attribute">
    <field name="attribute_id" options="{'no_create': True}"/>