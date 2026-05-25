# R-Project-Finding-GDP-Per-capita-and-Literacy-Rate

library(ggplot2)

gdp <- read.csv("worldbank_gdp_big.csv")
literacy <- read.csv("unesco_literacy_big.csv")

print(gdp)
print(literacy)

data <- merge(gdp, literacy, by = "Country")
print(data)

data <- na.omit(data)
print(data)

print("Summary Statistics for GDP per Capita and Literacy Rate:")
print(summary(data))

correlation_value <- cor(data$GDP_per_capita, data$Literacy_rate)

print("Correlation between GDP per Capita and Literacy Rate:")
print(correlation_value)

scatter_plot <- ggplot(data, aes(x = Literacy_rate, y = GDP_per_capita)) +
  geom_point(color = "blue", size = 3) +
  labs(
    title = "GDP per Capita vs Literacy Rate",
    x = "Literacy Rate (%)",
    y = "GDP per Capita (USD)"
  )

print(scatter_plot)

histogram2 <- ggplot(data, aes(x = GDP_per_capita)) +
  geom_histogram(
    binwidth = 1000,
    fill = "lightblue",
    color = "black"
  ) +
  labs(
    title = "Histogram of GDP per Capita",
    x = "GDP per Capita (USD)",
    y = "Frequency"
  )

print(histogram2)

histogram1 <- ggplot(data, aes(x = Literacy_rate)) +
  geom_histogram(
    binwidth = 5,
    fill = "lightgreen",
    color = "black"
  ) +
  labs(
    title = "Histogram of Literacy Rate",
    x = "Literacy Rate (%)",
    y = "Frequency"
  )

print(histogram1)

bar_chart <- ggplot(data, aes(x = Country, y = GDP_per_capita)) +
  geom_bar(
    stat = "identity",
    fill = "orange"
  ) +
  labs(
    title = "GDP per Capita for All Countries",
    x = "Country",
    y = "GDP per Capita (USD)"
  ) +
  theme(
    axis.text.x = element_text(
      angle = 90,
      hjust = 1
    )
  )

print(bar_chart)

ggsave(
  "scatter_plot.png",
  plot = scatter_plot,
  width = 8,
  height = 6
)

ggsave(
  "histogram_literacy.png",
  plot = histogram1,
  width = 8,
  height = 6
)

ggsave(
  "histogram_gdp.png",
  plot = histogram2,
  width = 8,
  height = 6
)

ggsave(
  "bar_chart.png",
  plot = bar_chart,
  width = 8,
  height = 6
)