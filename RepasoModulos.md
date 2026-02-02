# Repaso de los modulos de odoo
ejemplo de Selection:
```
from odoo import models, fields

class MiModelo(models.Model):
    _name = 'mi.modelo'

    estado = fields.Selection(
        selection=[
            ('draft', 'Borrador'),
            ('confirmado', 'Confirmado'),
            ('cancelado', 'Cancelado'),
        ],
        string='Estado',
        default='draft',
        required=True
    )
```
Lo llamariamos en la vista como cualquier otro, con el nombre de la variable:
```
<field name="estado"/>
```
---
Ejemplo de Many2one (muchos --> uno):
Un pedido pertenece a un cliente
```
class MiPedido(models.Model):
    _name = 'mi.pedido'

    partner_id = fields.Many2one(
        'res.partner',
        string='Cliente',
        required=True,
        ondelete='restrict'
    )
```
---
Ejemplo de One2many (uno --> muchos):
Un cliente tiene muchos pedidos
```
class ResPartner(models.Model):
    _inherit = 'res.partner'

    pedido_ids = fields.One2many(
        'mi.pedido',      # modelo hijo
        'partner_id',     # campo many2one en el hijo
        string='Pedidos'
    )
```
