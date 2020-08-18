# project_stylegan2

**Цель данной работы** - получение реалистичных и разнообразных изображений в хорошем качестве.  

Для решения поставленной задачи в данной работе использовалась архитектура StyleGAN2  для создания изображений людей в полный рост. Также была использована статья  "Interpreting the Latent Space of GANs for Semantic Face Editing". В качестве данных использовались изображения людей в полный рост на однотонном фоне, собранные с онлайн магазинов Wildberries и Lamoda. Был найден вектор направления изображения в латентном пространстве. С помощью найденного направления было произведено преобразование изображения.

* **parser_wildb_with_bbox** - парсинг wildberries.  

* **pars_lamoda** - парсинг lamoda.  

* **make_crop_mask_body_to_reid** - для того чтобы найти вектор направления изображения в латентном пространстве, необходимо разметить сгенерированные изображения. Для этого была использована сеть DensePose для сегментации частей тела. С помощью нее были получены маски частей тела людей. Для преобразования изображения берется только одна часть - туловище.  

* **embeddings_crops_body** - для получения признаков найденных масок с туловищами используется person re-identification для распознавания людей. Для решения данной задачи была использована библиотека Torchreid.  

* **svm_body_latents_find_direction** - с помощью латентного вектора опорного изображения необходимо преобразовывать изображение, сгенерированное с помощью StyleGAN2. Для этого необходимо разделить признаки в латентном пространстве с конкретным цветом одежды (берется латентный вектор туловища опорного изображения) и остальными признаками. Для классификации признаков использовался метод опорных векторов. После того как была найдена с помощью SVM разделяющая гиперплоскость в латентном пространстве, было найдено направление вектора у опорного изображения и с помощью него изменяли цвет одежды у сгенерированного изображения.

![](out4.gif)