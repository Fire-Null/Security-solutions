
### شناسایی پورت‌های باز


#### بستن پورت بر روی سرور ویندوزی(IIS)

```
تعدادی از پورت های مخرب:25 - 24 - 110 - 135 - 139 - 143 - 220 - 587 - 445 - 446 - 585 - 993 - 994 - 995 - 2390
```
* بستن پورت توسط CMD:

* CMD رو بازکنید و  این دستور رو تایپ کنید، فقط به جای Number عدد پورت مورد نظرتون رو وارد کنید تا بسته شود.

```ps
    netsh firewall delete portopening protocol = TCP port = number
```
