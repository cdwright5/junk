# junk
#Define characters
reg <- "([^A-Za-z\\d#@']|'(?![A-Za-z\\d#@]))"
#
#
AOC2 <- AOC2 %>%
  filter(!str_detect(text, '^"')) %>%
  mutate(text = str_replace_all(text, "https://t.co/[A-Za-z\\d]+|&amp;", "")) %>%
  unnest_tokens(word, text, token = "regex", pattern = reg) %>%
  filter(!word %in% stop_words$word,
         str_detect(word, "[a-z]"))

#By Month
AOCmonth <- AOC2 %>%
  count(word, month) %>%
  filter(sum(n) >= 5) %>%
  spread(month, n, fill = 0) %>%
  ungroup()

#Don't count as separate devices#
AOCwords <- tweet_words %>%
  count(word) %>%
  filter(sum(n) >= 5) %>%
  ungroup()
  
  txt txt
