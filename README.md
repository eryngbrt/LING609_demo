# LING609_demo
df <- read.table("gibsondata",header=TRUE,stringsAsFactors = FALSE,fileEncoding = "UTF-8")
head(df)
> head(df)
   subj item     type pos word correct   rt region            type2
7     1   13  obj-ext   6 抓住       - 1140    de1  object relative
20    1    6 subj-ext   6 男孩       - 1197    de1 subject relative
32    1    5  obj-ext   6   撞       -  756    de1  object relative
44    1    9  obj-ext   6 監視       -  643    de1  object relative
60    1   14 subj-ext   6 機師       -  860    de1 subject relative
73    1    4 subj-ext   6 男孩       -  868    de1 subject relative
install.packages("dplyr")
resultats <- df%>%
  filter(region=="headnoun",type%in% c("subj-ext", "obj-ext"))%>%group_by(type) %>%
  summarise(mean_RT = mean(rt,na.rm = TRUE), standard_error=sd(rt,na.rm = TRUE)/sqrt(sum(!is.na(rt))), n = sum(!is.na(rt)))
resultats
# A tibble: 2 × 4
  type     mean_RT standard_error     n
  <chr>      <dbl>          <dbl> <int>
1 obj-ext     487.           21.1   275
2 subj-ext    611.           46.7   272
