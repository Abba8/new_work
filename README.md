import matplotlib
import pandas as pd
import matplotlib.pyplot as plt
import matplotlib.ticker as mticker
matplotlib.use("TkAgg")

df=pd.read_excel('Məşğulluq.xlsx')



# amilləri götürürük
amiller = df["İnsanları fərqləndirən amillər"].unique()
fig, axes = plt.subplots(len(amiller), 1, figsize=(12, 16), sharex=True)

# Rəng palitrası (fərqli rənglər üçün)
colors = plt.cm.tab10.colors  # 10 fərqli rəng

for i, amil in enumerate(amiller):
    subset = df[df["İnsanları fərqləndirən amillər"] == amil]

    # Qrafik xətləri
    axes[i].plot(
        subset["Tarix"],
        subset["İnsanların sayı"],
        marker="o",
        color=colors[i % len(colors)],  # rəng
        linewidth=2,
        markersize=6,
        label=amil  # legend üçün
    )

    axes[i].grid(True)

    # Y-oxunda oxunaqlı rəqəmlər
    axes[i].yaxis.set_major_formatter(mticker.StrMethodFormatter('{x:,.0f}'))

    # Legend əlavə edirik
    axes[i].legend(loc="upper left", fontsize=9)

    # X-oxunu göstəririk
    plt.xlabel("İl", fontsize=12)
plt.tight_layout()
plt.show()
