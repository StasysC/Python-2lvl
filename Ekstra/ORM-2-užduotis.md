1. Su SQLAlchemy sukurkite modelį pagal šią diagramą:

![](https://github.com/robotautas/kursas/blob/master/DB/db4/uzduotis.png?raw=true)

kurdami many2many ryšį nenaudokite association table, vietoje jos sukurkite tarpinę lentelę kaip objektą, pagal tokį pavyzdį:

```python
class OrderProduct(Base):
    __tablename__='order_product'
    id = Column(Integer, primary_key=True)
    order_id = Column("order_id", Integer, ForeignKey('order_.id'))
    product_id = Column("project_id", Integer, ForeignKey('product.id'))
    quantity = Column("quantity", Integer)
    order = relationship("Order")
    product = relationship("Product")
```
2. Parašykite programą, kuri naudojantis jūsų sukurtu modeliu leistų:

* Pridėti pirkėją
* Pridėti produktą
* Pridėti statusą
* Pridėti užsakymą
* Ištraukti užsakymą pagal id
* Pakeisti užsakymo statusą pagal užsakymo id
* Pridėti į užsakymą produktus su kiekiais
 
