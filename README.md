def visualize_results(polarity, subjectivity, pos_counts, word_counts):
    """
    可视化分析结果
    """
    # 情感极性分布图
    plt.figure(figsize=(12, 5))
    
    plt.subplot(1, 2, 1)
    sentiments = ['Negative', 'Neutral', 'Positive']
    colors = ['red', 'gray', 'green']
    
    # 根据极性值分类
    if polarity < -0.3:
        index = 0
    elif polarity > 0.3:
        index = 2
    else:
        index = 1
    
    plt.bar(sentiments, [1, 1, 1], color=colors)
    plt.bar(sentiments[index], 1.2, color=colors[index])
    plt.title(f'Sentiment: {sentiments[index]} (Polarity={polarity:.2f})')
    
    # 词性分布饼图
    plt.subplot(1, 2, 2)
    labels = list(pos_counts.keys())
    sizes = list(pos_counts.values())
    
    # 简化标签显示
    pos_mapping = {
        'NN': 'Noun', 'VB': 'Verb', 'JJ': 'Adjective',
        'RB': 'Adverb', 'PRP': 'Pronoun', 'IN': 'Preposition'
    }
    labels = [pos_mapping.get(tag[:2], tag[:2]) for tag in labels]
    
    plt.pie(sizes, labels=labels, autopct='%1.1f%%', startangle=90)
    plt.title('Part-of-Speech Distribution')
    
    plt.tight_layout()
    plt.show()
    
    # 打印常用词
    print("\nTop 10 Words (excluding stopwords):")
    for word, count in word_counts:
        print(f"{word}: {count} times")
