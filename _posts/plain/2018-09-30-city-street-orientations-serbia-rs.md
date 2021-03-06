---
layout: post
title: Оријентација улица у градовима Србије
category: blog

gboeing-blog-url: https://geoffboeing.com/2018/07/comparing-city-street-orientations/
osmnx-install-url: https://geoffboeing.com/2016/11/osmnx-python-street-networks/
osmnx-repo: https://github.com/gboeing/osmnx
osmnx-example-repo: https://github.com/gboeing/osmnx-examples
osmnx-script-repo: https://github.com/28/osmnx-city-street-network-orientations
osmnx-paper-url: https://geoffboeing.com/publications/osmnx-complex-street-networks/
street-orientations-example-repo: https://github.com/gboeing/osmnx-examples/blob/master/notebooks/17-street-network-orientations.ipynb
gboeing-t: https://twitter.com/gboeing
belgrade-map: https://www.openstreetmap.org/#map=12/44.8084/20.5146
openstreetmap-url: https://www.openstreetmap.org
---

Видевши овај [пост]({{ page.gboeing-blog-url }}) на [Џеф Боинговом]({{ page.gboeing-t }}) блогу, одмах сам
пожелео да урадим сличну ствар са градовима по мом избору, а и да се поиграм са
одличним [*osmnx*]({{ page.osmnx-repo }}) алатом. Пожељно је прочитати овај пост пре настављања,
али у сваком случају ево сижеа.

### О *OSMnx* библиотеци ###

*OSMnx* је Python библиотека која омогућава лако добављање просторних геометрија
мрежа улица градова и држава над којим је могуће правити пројекције, визуализације,
анализе и сл. Ослања се на [OpenStreetMap]({{ page.openstreetmap-url }}) API.
Библиотека је добро структуирана тако да је могуће свашта нешто урадити са једном
или две линије кода.

На пример, да би се добио приказ мрежа улица Београда може да се уради овако нешто:
```python
import osmnx as ox
G = ox.graph_from_place('Belgrade, Serbia')
ox.plot_graph(G)
```

![Мрежа улица Београда](/public/img/street/belgrade_network.png "Мрежа улица Београда")

Ако нам треба нацрт административних граница, рецимо општине Нови Београд:
```python
G = ox.gdf_from_place('New Belgrade Municipality, Belgrade, Serbia')
ox.plot_shape(ox.project_gdf(G))
```

![Административна граница Новог Београда](/public/img/street/new_belgrade_shape.png "Административна граница Новог Београда")

Ово је само делић могућности ове библиотеке и саветујем да се погледа детаљније.
Пратите линкове из овог поста за више информација. Да се позабавимо оријентацијом улица...

### Оријентација улица ###

Једна од ствари које могу да се ураде уз помоћ ове библиотеке, а која је и
описана у поменутом блогу, јесте извлачење информација о оријентацији улица
у градовима. Оријентација подразумева правац простирања улице у односу на стране
света. Уз мало математике и других корисних Python библиотека могуће је представити
ове податке помоћу неког графика ради лакшег разумевања. У овом случају то је поларни
хистограм. На том графику правац сваке линије означава оријентацију у
односу на стране света, а дужина линије означава фреквенцију појављивања улица
са том оријентацијом.

Подешавање окружења за овај задатак је лако. Треба инсталирати *OSMnx* у Python
окружење помоћу *pip-а* или *conda-е*, а овај [пост]({{ page.osmnx-install-url }})
објашњава како. Постоји гомила примера коришћења ове библиоке у форми *Jupyter*
докумената [овде]({{ page.osmnx-example-repo }}). За израду ових графика коришћен
је [овај]({{ page.street-orientations-example-repo }}) пример мада сам га ја преписао у једну скрипту јер ми је било лакше.
Можете је наћи [овде]({{ page.osmnx-script-repo }})<sup id="f1r">[1](#f1)</sup>.

Наравно, [Београд]({{ page.belgrade-map }}) је био први на реду.

![Улице Београда](/public/img/street/belgrade.png "Улице Београда")

Након тога сам се одлучио да одрадим оријентације улица за све веће градове у
Србији. Пошто их је доста, поделио сам их у неколико целина<sup id="f2r">[2](#f2)</sup>.

Војводина:

![Улице Војводине](/public/img/street/vojvodina_s.png "Улице Војводине")

Централна Србија (са Београдом):

![Улице централне Србије](/public/img/street/central_s.png "Улице централне Србије")

Јужна Србија:

![Улице јужне Србије](/public/img/street/south_s.png "Улице јужне Србије")

Новопазарски регион:

![Улице новопазарског региона](/public/img/street/np_s.png "Улице новопазарског региона")

И Косово:

![Улице Косова](/public/img/street/kosovo_s.png "Улице Косова")

### Закључак ###

Србија је уникатна земља са јединственом геофрафијом и са јединственoм историјом.
Разни геополитички моменти су имали утицај на сваки вид живота њених грађана, а
један од њих је и сам начин на који су градови зидани. Распоред улица је различит
за скоро сваки град што се и види са приказаних слика. Сигуран сам да је могуће
пронаћи паралелу између облика/расподела улица једног града и народа који је ту
живео, као и разних историјских и политичких момената који су се ту појављивали.
По мом мишљењу ово је једна веома интересантна тема за изучавање.

Не покушавам да оставим посао незавршен односно да дигнем руке у стилу "ја сам
своје одрадио", али на први поглед има јако мало ресурса на Интернету који се
баве темом урбанизма у Србији тако да је тешко да се нађу подаци који би могли
да се упаре са овим сликама и информацијама које оне нуде. Са друге стране,
постоји доста књига на ову тему и покушаћу да их пронађем иако то захтева доста
времена. Све ново у односу на ову тему ћу писати овде. У међувремену надам се да
ће неко бити инспирисан да покрене било какво истраживање (или већ јесте...). Једна
ствар је сигурна - *OSMnx* је алат за тај посао.

Свака дискусија је добродошла на [Twitter-у]({{ site.twitter-url }}).

*Крај*

---
{% include footnote.html n=1 nid="f1" text="Може се приметити да сам за неке градове морао да
додајем кључну реч 'municipality' за добављање геоподатака. То је зато што информација за саме
градове није доступна па је критична област морала да се повећа. Ово може да утиче на сам крајњи
резултат јер се повећава и број улица које се испитују." r="#f1r" %}
{% include footnote.html n=2 nid="f2" text="Подела није рађена ни по каквом политичком,
религијском или етничком критеријуму, нашао сам да ми је оваква подела олакшавала посао." r="#f2r" %}
