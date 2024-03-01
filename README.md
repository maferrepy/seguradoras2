# seguradoras2
{
  "nbformat": 4,
  "nbformat_minor": 0,
  "metadata": {
    "colab": {
      "name": "Seguradors.ipynb",
      "provenance": [],
      "collapsed_sections": [],
      "authorship_tag": "ABX9TyMbtknXYD1ta0qqlkODiym2",
      "include_colab_link": true
    },
    "kernelspec": {
      "name": "python3",
      "display_name": "Python 3"
    },
    "language_info": {
      "name": "python"
    }
  },
  "cells": [
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "view-in-github",
        "colab_type": "text"
      },
      "source": [
        "<a href=\"https://colab.research.google.com/github/maferrepy/seguradoras2/blob/main/Seguradors.ipynb\" target=\"_parent\"><img src=\"https://colab.research.google.com/assets/colab-badge.svg\" alt=\"Open In Colab\"/></a>"
      ]
    },
    {
      "cell_type": "markdown",
      "source": [
        "# previsão de novos clientes.:"
      ],
      "metadata": {
        "id": "9SUbeRwbtmUr"
      }
    },
    {
      "cell_type": "code",
      "source": [
        "#modelagem de dados\n",
        "import pandas as pd\n",
        "\n",
        "# Matematica\n",
        "import numpy as np\n",
        "\n",
        "#Graficos\n",
        "import matplotlib.pyplot as plt\n",
        "import seaborn as sns\n",
        "\n",
        "#ignorar avisos\n",
        "from warnings import filterwarnings\n",
        "\n",
        "# Plano 1 = base de dados\n",
        "# Plano 2 = Novas entradas\n",
        "from matplotlib import colors\n"
      ],
      "metadata": {
        "id": "1xckw_6ctxD_"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "Base_dados = pd.read_excel('BaseDados_FlorestaDeDecisão.xlsx')\n",
        "\n",
        "# Não usou\n",
        "# Serviço\n",
        "# Furto"
      ],
      "metadata": {
        "id": "ZS3cg5uRvZ9-"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "Base_dados.head()"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 206
        },
        "id": "EtAgVnEYwHTD",
        "outputId": "b35ca770-10de-4537-fea8-332927a2597b"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "   Id Cliente  Idade  Preço Seguro    CEP  Serviço\n",
              "0           1     69          3930  19005        3\n",
              "1           2     27          3336  19027        1\n",
              "2           3     49          3936  19001        3\n",
              "3           4     60           157  19009        1\n",
              "4           5     51          3998  19050        2"
            ],
            "text/html": [
              "\n",
              "  <div id=\"df-458f4ed9-34cf-458f-b0ac-10769444190d\">\n",
              "    <div class=\"colab-df-container\">\n",
              "      <div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>Id Cliente</th>\n",
              "      <th>Idade</th>\n",
              "      <th>Preço Seguro</th>\n",
              "      <th>CEP</th>\n",
              "      <th>Serviço</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>1</td>\n",
              "      <td>69</td>\n",
              "      <td>3930</td>\n",
              "      <td>19005</td>\n",
              "      <td>3</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>2</td>\n",
              "      <td>27</td>\n",
              "      <td>3336</td>\n",
              "      <td>19027</td>\n",
              "      <td>1</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>3</td>\n",
              "      <td>49</td>\n",
              "      <td>3936</td>\n",
              "      <td>19001</td>\n",
              "      <td>3</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>4</td>\n",
              "      <td>60</td>\n",
              "      <td>157</td>\n",
              "      <td>19009</td>\n",
              "      <td>1</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>5</td>\n",
              "      <td>51</td>\n",
              "      <td>3998</td>\n",
              "      <td>19050</td>\n",
              "      <td>2</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>\n",
              "      <button class=\"colab-df-convert\" onclick=\"convertToInteractive('df-458f4ed9-34cf-458f-b0ac-10769444190d')\"\n",
              "              title=\"Convert this dataframe to an interactive table.\"\n",
              "              style=\"display:none;\">\n",
              "        \n",
              "  <svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\"viewBox=\"0 0 24 24\"\n",
              "       width=\"24px\">\n",
              "    <path d=\"M0 0h24v24H0V0z\" fill=\"none\"/>\n",
              "    <path d=\"M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z\"/><path d=\"M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z\"/>\n",
              "  </svg>\n",
              "      </button>\n",
              "      \n",
              "  <style>\n",
              "    .colab-df-container {\n",
              "      display:flex;\n",
              "      flex-wrap:wrap;\n",
              "      gap: 12px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert {\n",
              "      background-color: #E8F0FE;\n",
              "      border: none;\n",
              "      border-radius: 50%;\n",
              "      cursor: pointer;\n",
              "      display: none;\n",
              "      fill: #1967D2;\n",
              "      height: 32px;\n",
              "      padding: 0 0 0 0;\n",
              "      width: 32px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert:hover {\n",
              "      background-color: #E2EBFA;\n",
              "      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "      fill: #174EA6;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert {\n",
              "      background-color: #3B4455;\n",
              "      fill: #D2E3FC;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert:hover {\n",
              "      background-color: #434B5C;\n",
              "      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);\n",
              "      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));\n",
              "      fill: #FFFFFF;\n",
              "    }\n",
              "  </style>\n",
              "\n",
              "      <script>\n",
              "        const buttonEl =\n",
              "          document.querySelector('#df-458f4ed9-34cf-458f-b0ac-10769444190d button.colab-df-convert');\n",
              "        buttonEl.style.display =\n",
              "          google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "\n",
              "        async function convertToInteractive(key) {\n",
              "          const element = document.querySelector('#df-458f4ed9-34cf-458f-b0ac-10769444190d');\n",
              "          const dataTable =\n",
              "            await google.colab.kernel.invokeFunction('convertToInteractive',\n",
              "                                                     [key], {});\n",
              "          if (!dataTable) return;\n",
              "\n",
              "          const docLinkHtml = 'Like what you see? Visit the ' +\n",
              "            '<a target=\"_blank\" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'\n",
              "            + ' to learn more about interactive tables.';\n",
              "          element.innerHTML = '';\n",
              "          dataTable['output_type'] = 'display_data';\n",
              "          await google.colab.output.renderOutput(dataTable, element);\n",
              "          const docLink = document.createElement('div');\n",
              "          docLink.innerHTML = docLinkHtml;\n",
              "          element.appendChild(docLink);\n",
              "        }\n",
              "      </script>\n",
              "    </div>\n",
              "  </div>\n",
              "  "
            ]
          },
          "metadata": {},
          "execution_count": 5
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "Base_dados.info()"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "CVR9Ga98wLty",
        "outputId": "1499d54f-248f-4f98-9169-4edac58aff7f"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "<class 'pandas.core.frame.DataFrame'>\n",
            "RangeIndex: 500 entries, 0 to 499\n",
            "Data columns (total 5 columns):\n",
            " #   Column        Non-Null Count  Dtype\n",
            "---  ------        --------------  -----\n",
            " 0   Id Cliente    500 non-null    int64\n",
            " 1   Idade         500 non-null    int64\n",
            " 2   Preço Seguro  500 non-null    int64\n",
            " 3   CEP           500 non-null    int64\n",
            " 4   Serviço       500 non-null    int64\n",
            "dtypes: int64(5)\n",
            "memory usage: 19.7 KB\n"
          ]
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "Base_dados.isna().sum()"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "0Uo7JryGwZVL",
        "outputId": "178ccc9b-c735-4af7-b0ce-745e10091d62"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "Id Cliente      0\n",
              "Idade           0\n",
              "Preço Seguro    0\n",
              "CEP             0\n",
              "Serviço         0\n",
              "dtype: int64"
            ]
          },
          "metadata": {},
          "execution_count": 7
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "Base_dados.describe()"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 300
        },
        "id": "ISDWED3OwkWK",
        "outputId": "c4279195-03ec-4548-8526-9bc3b6b8fed4"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "       Id Cliente       Idade  Preço Seguro           CEP     Serviço\n",
              "count  500.000000  500.000000    500.000000    500.000000  500.000000\n",
              "mean   250.500000   49.550000   1939.268000  19024.812000    1.904000\n",
              "std    144.481833   18.167984   1402.289601     15.079105    0.858054\n",
              "min      1.000000   18.000000    100.000000  19000.000000    1.000000\n",
              "25%    125.750000   33.750000    612.000000  19011.000000    1.000000\n",
              "50%    250.500000   51.000000   1667.500000  19025.000000    2.000000\n",
              "75%    375.250000   65.000000   3329.500000  19038.000000    3.000000\n",
              "max    500.000000   80.000000   3998.000000  19050.000000    3.000000"
            ],
            "text/html": [
              "\n",
              "  <div id=\"df-e01381d3-4aa3-4544-b9ed-f2b7ff90b2cd\">\n",
              "    <div class=\"colab-df-container\">\n",
              "      <div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>Id Cliente</th>\n",
              "      <th>Idade</th>\n",
              "      <th>Preço Seguro</th>\n",
              "      <th>CEP</th>\n",
              "      <th>Serviço</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>count</th>\n",
              "      <td>500.000000</td>\n",
              "      <td>500.000000</td>\n",
              "      <td>500.000000</td>\n",
              "      <td>500.000000</td>\n",
              "      <td>500.000000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>mean</th>\n",
              "      <td>250.500000</td>\n",
              "      <td>49.550000</td>\n",
              "      <td>1939.268000</td>\n",
              "      <td>19024.812000</td>\n",
              "      <td>1.904000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>std</th>\n",
              "      <td>144.481833</td>\n",
              "      <td>18.167984</td>\n",
              "      <td>1402.289601</td>\n",
              "      <td>15.079105</td>\n",
              "      <td>0.858054</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>min</th>\n",
              "      <td>1.000000</td>\n",
              "      <td>18.000000</td>\n",
              "      <td>100.000000</td>\n",
              "      <td>19000.000000</td>\n",
              "      <td>1.000000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>25%</th>\n",
              "      <td>125.750000</td>\n",
              "      <td>33.750000</td>\n",
              "      <td>612.000000</td>\n",
              "      <td>19011.000000</td>\n",
              "      <td>1.000000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>50%</th>\n",
              "      <td>250.500000</td>\n",
              "      <td>51.000000</td>\n",
              "      <td>1667.500000</td>\n",
              "      <td>19025.000000</td>\n",
              "      <td>2.000000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>75%</th>\n",
              "      <td>375.250000</td>\n",
              "      <td>65.000000</td>\n",
              "      <td>3329.500000</td>\n",
              "      <td>19038.000000</td>\n",
              "      <td>3.000000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>max</th>\n",
              "      <td>500.000000</td>\n",
              "      <td>80.000000</td>\n",
              "      <td>3998.000000</td>\n",
              "      <td>19050.000000</td>\n",
              "      <td>3.000000</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>\n",
              "      <button class=\"colab-df-convert\" onclick=\"convertToInteractive('df-e01381d3-4aa3-4544-b9ed-f2b7ff90b2cd')\"\n",
              "              title=\"Convert this dataframe to an interactive table.\"\n",
              "              style=\"display:none;\">\n",
              "        \n",
              "  <svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\"viewBox=\"0 0 24 24\"\n",
              "       width=\"24px\">\n",
              "    <path d=\"M0 0h24v24H0V0z\" fill=\"none\"/>\n",
              "    <path d=\"M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z\"/><path d=\"M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z\"/>\n",
              "  </svg>\n",
              "      </button>\n",
              "      \n",
              "  <style>\n",
              "    .colab-df-container {\n",
              "      display:flex;\n",
              "      flex-wrap:wrap;\n",
              "      gap: 12px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert {\n",
              "      background-color: #E8F0FE;\n",
              "      border: none;\n",
              "      border-radius: 50%;\n",
              "      cursor: pointer;\n",
              "      display: none;\n",
              "      fill: #1967D2;\n",
              "      height: 32px;\n",
              "      padding: 0 0 0 0;\n",
              "      width: 32px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert:hover {\n",
              "      background-color: #E2EBFA;\n",
              "      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "      fill: #174EA6;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert {\n",
              "      background-color: #3B4455;\n",
              "      fill: #D2E3FC;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert:hover {\n",
              "      background-color: #434B5C;\n",
              "      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);\n",
              "      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));\n",
              "      fill: #FFFFFF;\n",
              "    }\n",
              "  </style>\n",
              "\n",
              "      <script>\n",
              "        const buttonEl =\n",
              "          document.querySelector('#df-e01381d3-4aa3-4544-b9ed-f2b7ff90b2cd button.colab-df-convert');\n",
              "        buttonEl.style.display =\n",
              "          google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "\n",
              "        async function convertToInteractive(key) {\n",
              "          const element = document.querySelector('#df-e01381d3-4aa3-4544-b9ed-f2b7ff90b2cd');\n",
              "          const dataTable =\n",
              "            await google.colab.kernel.invokeFunction('convertToInteractive',\n",
              "                                                     [key], {});\n",
              "          if (!dataTable) return;\n",
              "\n",
              "          const docLinkHtml = 'Like what you see? Visit the ' +\n",
              "            '<a target=\"_blank\" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'\n",
              "            + ' to learn more about interactive tables.';\n",
              "          element.innerHTML = '';\n",
              "          dataTable['output_type'] = 'display_data';\n",
              "          await google.colab.output.renderOutput(dataTable, element);\n",
              "          const docLink = document.createElement('div');\n",
              "          docLink.innerHTML = docLinkHtml;\n",
              "          element.appendChild(docLink);\n",
              "        }\n",
              "      </script>\n",
              "    </div>\n",
              "  </div>\n",
              "  "
            ]
          },
          "metadata": {},
          "execution_count": 8
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "# font_scale = 1.5> 'tamanho da fonte'\n",
        "#rc={'figure.figsize':(20,20)}) = tamanho da figura\n",
        "# bins=20 =  largura do grafico\n",
        "#colors= 'purple'= cor do grafico"
      ],
      "metadata": {
        "id": "R7cERX04xS4w"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "sns.set(font_scale=1.5, rc={'figure.figsize':(20,20)})\n",
        "eixo = Base_dados.hist(bins=20, color= 'red')"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 1000
        },
        "id": "y8zucp0IxR9b",
        "outputId": "c950965b-4696-4c71-933b-9f3c9cb0c7d7"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "display_data",
          "data": {
            "text/plain": [
              "<Figure size 1440x1440 with 6 Axes>"
            ],
            "image/png": "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euWVVyTVgrkxYHz66adGfHy8sWTJEt+yoqIiIyUlxRg9erRzjdUB+fn5xpkzZwzDMIzNmzcb8fHxxs6dOyuMS01NNQYPHmyUlpb6ls2ePdu45ZZbjGPHjvmW/fnPfzbi4+ONzZs3+5bl5eUZd9xxh/H000/b90JqqV27dhnFxcV+y44dO2Z07tzZeOaZZ3zLfvjDHxr33XefUVBQ4Fv27rvvGvHx8cbHH3/sW8Z7/dsVFhYa99xzjzFx4kTfMubXGs8884yRlpZmjBkzxnjooYf81jHH5uzcubPC78zKML9A5azezga7mmwjg5kV27dgYfV2KdicP3/eSE5ONn75y19ed1xV/3YKdv/7v/9rxMfHG2+++aZvWX187yxYsMCIj483jhw54rd80qRJxq233mqUlJQYhuH83HBanKQPPvhAoaGhGjZsmG9Zo0aN9PDDD2vXrl06deqUg93VblFRUYqJibnumKNHj+ro0aMaMWKEGjRo4Fs+evRolZeXa9OmTb5lH374oVq0aKEHHnjAt6x58+bq16+ftmzZokuXLln/Imqxrl27KiwszG9Z27Zt1bFjR9+hxQUFBfr44481aNAgRUZG+sYNHDhQERER2rhxo28Z7/Vv17hxYzVv3lznz5+XxPxaZd++fVq3bp2effbZCuuYY2sUFBRUerg88wtcm9Xb2WBXk21ksLJq+xaMrNguBZv169fr/PnzevLJJyVdngvDMPzGVOdvp2C3YcMGhYSEqH///pLq73vnwoULkqTY2Fi/5d/5znfUsGFDNWjQoFbMDeGSLh8+1q5dO79vgiR16dJFhmHU2+v9WOXgwYOSpM6dO/stb9mypVq1auVbL13+XiQkJCgkJMRv7G233aYLFy7oX//6l/0N13KGYej06dO+UC87O1ulpaUV5jcsLEydOnXye//yXq9cQUGBzpw5o3/+85+aPXu2jhw54jssl/mtOcMw9Mtf/lKDBg1Sp06dKqxnjmvu6aefVrdu3XT77bfrkUceUXZ2tm8d8wtUT022s8HIqm1kMLJy+xZsrNouBZsdO3aoffv2+uijj/S9731P3bp101133aWZM2eqrKxMUvX+dgpmly5d0saNG5WUlKQbb7xRUv1979x5552SpOeff16HDx/Wv//9b61bt8536QKXy1Ur5oZrLunyedJXnwN8hdvtliQ+qa0hr9cr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37+/PTjKzc3VuHHj1KxZM40cOVK33367Dh8+rJycHO3bt085OTlq0qSJJCk/P18PP/ywCgsLlZqaqtjYWF26dEmff/65du3apd69e0uSduzYoZ/85Ce69dZbNX78eIWGhurPf/6z5s6dq/z8fM2cOfO6Y2jTpo0kaePGjUpISFDTpk2v2/7UqVMaOXKkKioqNGzYMN1xxx36+uuvtWrVKu3Zs0fvvPOOwsLCJF0O0h555BFVV1crLS1Nt99+uz788EM9+uijTsx2TcXFxRozZozi4+OVkZGhc+fOSZK++OILpaWlyd/fX4888ohuvfVW7dy5U5mZmTp8+LBeeuklQ34/AACAK23ZskWSNHLkyHofe+V70bc1a9bMvj7T9Y69ePHiNa/KB9B4ES4BHuDSpUv2D+ozZ87oj3/8ow4fPqy4uDi1a9fO3i4/P1/PPvushg8f7nD8U089JZPJpHXr1jncvpWQkKCf/OQn2rRpkx566CFJ0m9+8xudOXNGS5cu1f333+/QT3V1tSSpqqpK8+bNU3BwsNauXavbb79d0uXb9caOHas33nhDQ4YMcajt2xITExUTE6O//OUv+tvf/qbu3bvr7rvvVnx8vP7nf/7HHnZdMW/ePFVWVmrDhg1q2bKlfXtycrJGjhypP/zhD3rsscckSS+//LKsVqv+9Kc/2a8qGjNmjDIyMnTw4MHvnO/vcv78eU2dOrVGgPbb3/5W5eXlWr16tbp06eLwe9977z0NGzbsmldqAQAANBZffvmlQkND7ScD66qkpOSa33XWrVvncAucdHlpgXPnztnXXFqwYIGqq6s1ePBgp2sH4B6ES4AHePXVV/Xqq6/af/b19VW/fv1qLObdvHlze0h0xZEjR3TkyBE99thjKi8vdzib1L17dwUHB+vjjz/WQw89pPPnz+tvf/ub7r///hrB0pXfK0kHDx7UqVOnlJ6ebg+WpMuLOD766KOaPn26tm/frokTJ15zTAEBAcrJydGKFSu0efNmffjhh/rggw8kSREREZozZ479tr6ioiJ98MEHeuihhxQQEOAwhsjISN1xxx36+OOP9dhjj6mqqkofffSR7rnnHofb1SRpwoQJ2rx58zVrqo9vj62wsFD79u3Tj370I3uwJF1++sm0adP0/vvv669//SvhEgAAaPSsVqsiIiLqfVxgYKCysrJq3XfnnXfW2Jaenu7wc1BQkMaPH68ZM2bU+3cDcC/CJcADjBw5UsnJyfLx8VFQUJDatWun5s2b12jXpk0b+fn5OWw7fvy4pJoB1dXOnj0rSfr3v/8tm82mu+6667r15OfnS5I6duxYY1+nTp0kyb4W1PWEhIRo2rRpmjZtmqxWqw4cOKBt27bp7bff1hNPPKHIyEh1795dX331laqrq7Vu3TqtW7eu1r6unFk7d+6cSkpKav0CU9s2Z4SHh6tZs2YO2643J+3bt5evr2+d5gQAAMDdQkNDVVxcXO/j/Pz81KtXrzq3/+Uvf6k777xTPj4+atasmTp06PCdSyUAaJwIlwAP0LZt2zp9UAcFBV1z34QJE2q9GklSjaDEHUJDQ9WrVy/16tVLXbp00dNPP63169ere/fustlskqRBgwZpyJAhtR4fGBjo1O/18fG55r7Kyspat19vngEAADxdp06d9Omnn+rkyZP1vjWuPu65554at8oB8EyES4CXa9u2raTLt7R9V0B1xx13yMfHR3l5eddtFxUVJUk6duxYjX1Xtt3IF5Hvfe97kqTTp0871FVRUfGdYwgPD1dwcLC++uqrGvtq23bLLbdIki5cuFBj35WrkerienPyr3/9S9XV1S79cgYAAGCU/v3769NPP9XatWs1a9Ysd5cDwAP4ursAAK511113qXPnzlq9enWtt2VVVlbq/Pnzki6v2dSnTx999NFH2rVrV422V64giomJUevWrbV+/XpZLBb7/oqKCr355pvy8fFRYmLidevKy8vTmTNnat23bds2Sf+9xaxFixb6wQ9+oL/+9a/av39/rXVdWYfJz89P999/vw4cOKB//vOfDu2WLVtW49ioqCj5+/vXGO/evXtr/V3XEhERoW7dumnnzp06evSoQ21vvPGGJOlHP/pRnfsDAABwl+HDh+vOO+/UsmXL7N/Lvi03N1crV65s4MoANFZcuQR4OR8fH73wwgsaN26cBg0apKFDh6pjx44qLS3V119/rb/+9a+aNWuWfSHwp59+WocOHdKkSZM0ePBgxcTEqKysTJ9//rkiIyP1+OOPy8/PT08//bR+8pOfaNiwYRoxYoRCQkK0efNm7d+/X1OnTr3uk+IkadeuXXr55ZfVu3dvxcfH69Zbb1VRUZE++eQT7dixQyaTSePHj7e3//Wvf63Ro0drzJgxSk1N1V133aXq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AEANeSVcyszM1Keffqrf/va3mjlzppKTk/X++++rXbt2mj9/vjeGBAAAAAAAAAO8Ei5t27ZNAQEBevDBB51tTZo00X/9138pIyNDZ8+e9cawAAAAAAAAUENeCZeysrLUpUsXtWjRwqW9T58+cjgcysrK8sawAAAAAAAAUEONvfGmNptN4eHhldotFosk1fibS/7+fh4ZVyWdOplyWdPG62NjMFNDrq8h18aa803UZjIfWRf14rMCAACAV3glXCouLlZAQECl9iZNmkiSSkpKanS9kJAWN+9kxA8/mHLZNm2CTLmur43BTA25voZcG2vON1GbyRrwugAAAEDD4JXb4po2baqysrJK7eWhUnnIBAAAAAAAgPrNK+GSxWJxe+ubzWaTJIWFhdX1kAAAAAAAAGCAV8Kl7t2768SJEyosLHRpP3TokPM4AAAAAAAA6j+vhEsJCQkqKyvTunXrnG2lpaX661//qtjYWLebfQMAAAAAAKD+8cqG3n379lVCQoLmz58vm82mjh07asOGDTp9+rReeeUVbwwJAAAAAAAABvg5HA6HN964pKREb7zxhjZt2qT8/HxZrVb95je/0aBBg7wxHAAAAAAAABjgtXAJAAAAAAAAvs8rey4BAAAAAACgYSBcAgAAAAAAgGGESwAAAAAAADDMK0+Lqwtnz57VypUrdejQIR0+fFhFRUVauXKlBgwYUK3zs7Oz9fLLL+vgwYMKCAjQkCFDNGvWLIWGhrr0s9vtSk1N1erVq2Wz2dS5c2c99dRTSkxMNKMsScZrs9vt2rBhgz777DNlZWUpPz9f7du3V1JSkiZMmKDAwEBn31OnTmnYsGFur7NkyRLdddddHq2pXG3mbfbs2dqwYUOl9r59++qjjz5yafOleZMkq9Va5bFBgwZp+fLlkrw3b5mZmdqwYYPS09N1+vRptW7dWjExMZo2bZo6dep00/Pz8vL08ssva8+ePbLb7brjjjv0/PPPq0OHDpX6rlu3TsuWLdOpU6cUERGhlJQUPfLII2aUJal2te3YsUNbtmxRZmamzp8/r3bt2mnIkCH69a9/reDgYJe+Vc3x73//ez388MMeq+d6tantrbfe0qJFiyq133LLLdqzZ0+ldl+at6FDh+rHH390e6xTp07asWOH87U35u1///d/tXjxYh09elTnz59XcHCwunfvrqefflqxsbE3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vfbaa7r33nvl5+dX67HfTE1qe/TRR11eJyQkqFu3bpo7d64++eQTPfTQQ5J8f97sdrs+/fRT3XbbbW43AffmvD399NNKTk5Wbm6u0tLSVFpaqrKyMrfrSfLN9QYAAADfwG1xFZT/gO1ur5ryH6bLn4bUtGnTG/ar+CSo+mbLli164403lJycrOTk5Jv2Dw8P17333qtDhw45b52o78qfaLR3715nm6/P2/bt21VSUqKRI0dWq39dz5vNZtPkyZPVqlUrLVy4UP7+Vf8144n1Vt63LuatJrVVdODAAb3wwgsaPHiwnn322Zv2b968ucaMGaPc3Fx9//33tRl2tdSmtnIPP/ywmjVrVq31JvnGvO3fv195eXnVXm91OW9Wq1V33nmnHnjgAaWmpurIkSN6/vnnq+zva+sNAAAAvoNwqYKwsDBJP/0yUpHNZlObNm3UqFEjST/dRlC+f0rFftdfqz7as2ePZs6cqSFDhuill16q9nnt2rWT3W6/6aax9cUtt9yigIAA5efnO9t8ed6kn779EhwcrCFDhlT7nLqat8uXL2vixIm6fPmyli5d6vb2m+u1bt1agYGBVa43Pz8/5zUsFovKysoq7elTWlqqixcvmj5vNa3tev/4xz/01FNPyWq1asGCBc6/Q26mXbt2kuTy59cMtantev7+/goPD6+03nx13qSf1pu/v7/uvffeap9TV/N2vYCAAA0bNkw7duxwfvuoIl9abwAAAPAthEsVhIeHKzQ0VIcPH650LDMzUz169HC+7tGjhwoKCnTixAmXfocOHXIer48OHTqkqVOnqnfv3jX6RVeScnJy1KhRI7Vq1crEEXpObm6uysrKFBoa6mzz1XmTftoPKj09Xffcc0+Vt764UxfzVlJSoilTpuiHH37Qu+++q65du970HH9/f0VFRVW53jp16qRmzZpJ+ve8VOx7+PBh2e12U+fNSG3lTp48qSeffFKhoaF699131bx582qfm5OTI0kuf349rTa1VVRWVqYzZ864bJjtq/Mm/fupjP3793d5eujN1MW8uVNcXCyHw6HCwkK3x31lvQEAAMD3/OzDpZMnT+rkyZMubffcc492796tvLw8Z9vevXv1ww8/KCEhwdk2bNgwBQQE6MMPP3S2ORwOrVmzRhEREerbt6/5BdyAu9qys7M1adIkRUZGavHixc5bICq6cOFCpbZ//etf+vTTT3X77bdXeV5dqVhbSUmJCgoKKvV75513JMlls3JfnLdyW7Zskd1ur/IWHW/N27Vr1zRt2jR9++23WrhwoaKjo932O336dKXHwA8fPlzffvuty9Onvv/+e+3bt89lvd1xxx1q3bq1y7xJ0urVq9W8eXPdddddHqzo32pTm81m04QJE+Tn56fU1NQqwwZ38/Z///d/+vDDD9W+fXt17ty51nW4U5va3I05NTVVJSUl+o//+A9nmy/OW7nypzLWZL3Vxby5e9+CggJt375d7dq1U5s2bST55noDAACAb2rQG3qXBwvlP1ynpaUpIyNDLVu21Lhx4yRJjz32mCRp9+7dzvOmTJmibdu2KSUlRePGjVNRUZFSU1PVvXt3l41g27Ztq5SUFC1btkwlJSXq3bu3du7cqQMHDmjBggWG9iwxs7aCggI98cQTunTpkp544gl98cUXLte0Wq3q3r27JOm1115TTk6O7rjjDoWFhenkyZPOjWtnzZplWl1Ga7PZbM6NdLt27ep8WtzevXuVmJioX/7yl87r+9q8XW/jxo0KCwvTgAED3F7fW/M2b9487d69W0OGDNHFixeVlpbmPNaiRQvFx8c7x7B//34dO3bMeXzs2LFat26dJk2apMcff1yNGjXSihUrZLFYnJ+F9NMeMP/93/+tuXPn6tlnn1VcXJwOHDigjRs36re//W2lzc3rQ21PPvmkcnJy9OSTTyojI0MZGRnOYx07dlRMTIwkadWqVdq1a5cGDx6siIgI5eXlae3atbpw4YLefvttU+qqbW1DhgxRYmKioqKiFBgYqPT0dG3fvl39+vVzeUqaL85buaqeyljOW/M2bdo0NWnSRDExMbJYLDpz5oz++te/Kjc3V6+//rqzny+uNwAAAPgmP4fD4fD2IMxitVrdtkdGRjp/cR86dKikyr/I//Of/9S8efOUkZGhgIAADR48WM8//3ylbx7Y7XYtWbJEa9eu1dmzZ9WlSxdNnjzZ9EdQG6nt1KlTGjZsWJXXnDp1qp555hlJ0ubNm7VmzRodP35cly9fVsuWLdW/f39NnTpV3bp182QplRip7dKlS/rjH/+oQ4cO6ezZs7Lb7ercubNGjx6tlJSUSrf++dK8lfv+++81YsQIPf7445o9e7bb63hr3saPH6/9+/e7PXZ9beX9Kv4in5ubq5dffll79uyR3W7XgAED9MILL6hDhw6VrvfRRx9p2bJlOnXqlNq1a6fx48crJSXF80X9f7Wprar5ln56qti8efMkSV9//bVSU1P13XffKT8/X82bN1d0dLQmT56sfv36ebAaV7Wp7Xe/+50OHjyoM2fOqKysTJGRkUpMTNTkyZPdfkPOl+ZN+imMHzRokH71q1/prbfecnsdb83b+vXrlZaWpuPHj+vSpUsKDg5WdHS0JkyYoP79+zv7+eJ6AwAAgG9q0OESAAAAAAAAzPWz33MJAAAAAAAAxhEuAQAAAAAAwDDCJQAAAAAAABhGuAQAAAAAAADDCJcAAAAAAABgGOESAAAAAAAADCNcAgAAAAAAgGGESwAAAAAAADCMcAkAAAAAAACGES4BAAAAAADAsP8HhYiAvqAxwv0AAAAASUVORK5CYII=\n"
          },
          "metadata": {}
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "#Graficos boox"
      ],
      "metadata": {
        "id": "IvmyRvFA1l-e"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "plt.figure(figsize= (10,5))\n",
        "sns.boxplot(data = Base_dados , x = 'Serviço', y= 'Idade');"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 352
        },
        "id": "ceFWUTdW0TUe",
        "outputId": "777f9396-ccba-4fcb-f77c-e2a292d0517e"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "display_data",
          "data": {
            "text/plain": [
              "<Figure size 720x360 with 1 Axes>"
            ],
            "image/png": "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\n"
          },
          "metadata": {}
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "# o grafico mostra que pessoas de menos idade usam menos os serviços \n",
        "# pessoas com idade mais avançada usam mais serviços de reparo\n"
      ],
      "metadata": {
        "id": "FtbMDpTT0tYW"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "plt.figure(figsize= (10,5))\n",
        "sns.boxplot(data = Base_dados , x = 'Serviço', y= 'CEP');"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 338
        },
        "id": "0nJTlAwA2KSK",
        "outputId": "ea6e3d9b-0b22-4ae1-83f0-0e7562131afd"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "display_data",
          "data": {
            "text/plain": [
              "<Figure size 720x360 with 1 Axes>"
            ],
            "image/png": "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gFblqqaw6+vrW7oPAAAAtBHcAwkAAABDCJAAAAAwhAAJAAAAQ5oVIF1cXJq1DQAAAO1fs77KcNGiRVqyZInDtvj4eLm6OubPurq6lusMAAAArVKTAXLEiBE3og8AAAC0EU0GyA0bNtyIPgAAANBG8BANAAAADGkyQNbV1WnlypXauHFjo+NSU1P1+uuvs8g4AABAO9dkgPzwww/1zjvvKDQ0tNFxd955p9auXas//OEPLdYcAAAAWp8mA2RmZqbuueceDRkypNFxQ4YMUUREhD766KMWaw4AAACtT5MB8osvvtDo0aObVWzkyJE6dOjQNTcFAACA1qvJAHn27Fn16tWrWcV69uyp0tLSa24KAAAArVeTAbJbt276/vvvm1WstLRU3bp1u+amAAAA0Ho1uQ7k7bffruzsbD3xxBNNFsvOztbtt9/eIo3hys6eLVVdVakqC3aY3QragbqqUp0926wvpbqhzp4t1fflF/RfuSVmt4J24HT5BfmeZYYMaClNXoF86KGHtGvXLmVlZTU6bseOHdq1a5d++MMftlhzAAAAaH2avOzw2GOPaePGjXruuef05JNP6tFHH1Xfvn3t7588eVJpaWl69913FRgYqMcee+y6NgzJ29tH1nMX1DVgnNmtoB2oLNghb28fs9tw4u3to07nv1PcnT3NbgXtwH/llqhzKzzPgbaqyQDZuXNnvf322/rpT3+qt956S2+//ba8vLzUrVs3VVRUqLy8XPX19erfv7/eeustderU6Ub0DQAAAJM068angIAAZWRk6P3339e2bdv0f//3f/ruu+/UrVs3DR8+XD/84Q/16KOPqnPnzte7XwAAAJis2XfOd+rUSTExMYqJibme/QAAAKCVa/IhmuvpzJkzWrlypWJiYhQeHq7g4GDt3r3baVxZWZmWLl2qiIgIhYaGasqUKdq6dWuDNYuKipSQkKDhw4dr6NChmjNnjgoLCx3GfPvtt3rzzTf1yCOPaMSIERo5cqRiYmL0t7/97aprAgAAdBSmBsgTJ05o7dq1KioqUnBwcINjLly4oLi4OKWlpWnSpEl66aWX1LdvX82fP1/p6ekOYysqKhQbG6u9e/cqPj5e8+bNU15enmJjY3X27Fn7uB07dmjdunUKCAjQc889pzlz5qiiokKzZ8++6poAAAAdhamLv4WEhCgnJ0e+vr7KysrS3Llz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b775Rp999pnS0tK0Z88ezZkzR5s3b9axY8ckSbNnz75ine+++87hdb9+/eTm5uY07lJI3Lp1q1544QW5urrqs88+0zfffKOf//znjfb69ddfq76+XoMHD2503MmTJyXJ4QrnJXfccYck2cMxgI6FAAkALczPz09+fn6aOnWqoqKitG/fPuXm5urSqmlJSUm6+eabG9z38ulrSerSpcsVjzN16lQtX75cOTk5uueee5Seni43NzdNmTKl5f4yANAAAiQAXCcuLi666667tG/fPp05c8Z+r6Cvr6/uueeea64/efJkvfrqq0pPT9fQoUO1bds23XPPPVcMp5f4+/vLxcVFX375ZaPj+vbtK0n66quvnN67tO2fAy+AjoF7IAHgGmVnZ+vChQtO26uqquxL4gQFBWnixIny9PTUm2++qaqqKqfxZWVlqqmpafZxe/bsqTFjxujjjz/W1q1bVV5e3uTDM9LF+yrvu+8+ffrpp073XEqyXykNCQnRrbfeqi1btjisZVlbW6t33nlHLi4uGjduXLP7BdB+cAUSAK7Rr371K5WWluqBBx7QgAED1LlzZ50+fVpbt25Vfn6+pk2bZl+H8Re/+IUSExMVGRmpKVOmyM/PTyUlJTp69KiysrL00Ucf2a/8Ncf06dP1ySef6JVXXlH37t314IMPNmu/xYsXKy8vT0899ZSmTZumkJAQVVdX6/PPP5efn59+/vOfy83NTYsXL9YzzzyjRx55RD/+8Y/VrVs3ZWZm6sCBA4qPj+cJbKCDIkACwDVauHChduzYob1792rbtm0qKytT9+7dNWDAAD311FMOT1HPmDFDgYGBevfdd7Vp0yaVlZXJx8dH/fv3V0JCgtOi4025//775ePjo9LSUj366KPN/rrCfv36afPmzVq9erU+/fRTffDBB5Kke++9VzNnzrSPe+CBB5SSkqI1a9bonXfeUW1trYKCghpcWghAx8F3YQMA9MEHH+jDDz+84rfbAMDluAcSAKDx48dr9+7dOnHihNmtAGgDmMIGgA7sb3/7m06cOGFfz9HIQzwAOi4CJAB0YKWlpXr99ddVV1enmTNn2h/2AYDGcA8kAAAADOEeSAAAABhCgAQAAIAhBEgAAAAYQoAEAACAIQRIAAAAGPL/AE7vDohigGWxAAAAAElFTkSuQmCC\n"
          },
          "metadata": {}
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "caracteristicas= Base_dados.iloc[:,1:4].values\n",
        "previsor = Base_dados.iloc[:,4:5]. values\n"
      ],
      "metadata": {
        "id": "38MWVeW63CyR"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "from sklearn.model_selection import train_test_split"
      ],
      "metadata": {
        "id": "Gqs4mho74GIv"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "from pandas.core.common import random_state\n",
        "x_treinamenos,x_teste, Y_treinamento, y_teste = train_test_split(\n",
        "    caracteristicas,\n",
        "    previsor,\n",
        "    test_size=0.30,\n",
        "    random_state = 10\n",
        "    \n",
        ")\n",
        "print(len(Base_dados))\n",
        "print(len(x_treinamenos))\n",
        "print(len(x_teste))"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "5n-8EVP-4Ob5",
        "outputId": "c935113e-f267-4b61-ad0a-73f7c045de61"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "500\n",
            "350\n",
            "150\n"
          ]
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "from sklearn.ensemble import RandomForestClassifier"
      ],
      "metadata": {
        "id": "yCkCp2bC498y"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "floresta1 = RandomForestClassifier( n_estimators= 500)"
      ],
      "metadata": {
        "id": "QdMmm0_G52wi"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "floresta1.fit(x_treinamenos, Y_treinamento)"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "QUVAev_26ACw",
        "outputId": "387a942a-355e-4f8c-a13c-fb65007a80d8"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stderr",
          "text": [
            "/usr/local/lib/python3.7/dist-packages/ipykernel_launcher.py:1: DataConversionWarning: A column-vector y was passed when a 1d array was expected. Please change the shape of y to (n_samples,), for example using ravel().\n",
            "  \"\"\"Entry point for launching an IPython kernel.\n"
          ]
        },
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "RandomForestClassifier(n_estimators=500)"
            ]
          },
          "metadata": {},
          "execution_count": 44
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "previsao = floresta1.predict(x_teste)\n",
        "from sklearn.metrics import confusion_matrix                                       \n",
        "Matriz_confusão =confusion_matrix( y_teste, previsao)\n",
        "print(Matriz_confusão)\n",
        "plt.figure(figsize=(10,5))\n",
        "sns.heatmap(Matriz_confusão, annot= True)\n"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 410
        },
        "id": "6cptpW0H6zrT",
        "outputId": "a367dcfa-9cee-4a05-a182-8f647aec0c4a"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "[[60  3  1]\n",
            " [ 7 22  7]\n",
            " [ 0  1 49]]\n"
          ]
        },
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "<matplotlib.axes._subplots.AxesSubplot at 0x7f988dc65b90>"
            ]
          },
          "metadata": {},
          "execution_count": 47
        },
        {
          "output_type": "display_data",
          "data": {
            "text/plain": [
              "<Figure size 720x360 with 2 Axes>"
            ],
            "image/png": "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\n"
          },
          "metadata": {}
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "# medir a acuracia.\n",
        "from sklearn.metrics import classification_report\n",
        "report = classification_report(y_teste, previsao)\n",
        "print(report)\n"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "OkPDiCAX9q0W",
        "outputId": "3294356e-2d28-4755-f09c-f7b523275755"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "              precision    recall  f1-score   support\n",
            "\n",
            "           1       0.90      0.94      0.92        64\n",
            "           2       0.85      0.61      0.71        36\n",
            "           3       0.86      0.98      0.92        50\n",
            "\n",
            "    accuracy                           0.87       150\n",
            "   macro avg       0.87      0.84      0.85       150\n",
            "weighted avg       0.87      0.87      0.87       150\n",
            "\n"
          ]
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "#quais clientes vão usar seguro"
      ],
      "metadata": {
        "id": "7_G5DZWv-mN_"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "Novas_vendas = pd.read_excel('BaseDados_FlorestaDeDecisão.xlsx', 'Plan2')\n",
        "Novas_vendas.head()"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 206
        },
        "id": "aw7qs3RQ-wBN",
        "outputId": "09be1633-8388-4618-8ccb-d82d54c58337"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "   Id Cliente  Idade  Preço Seguro    CEP\n",
              "0        1001     25           801  19001\n",
              "1        1002     27          1090  19027\n",
              "2        1003     45           364  19030\n",
              "3        1004     30          2428  19014\n",
              "4        1005     32           891  19020"
            ],
            "text/html": [
              "\n",
              "  <div id=\"df-1a69c10a-56b5-4b7c-884e-bfb2b438b1a0\">\n",
              "    <div class=\"colab-df-container\">\n",
              "      <div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>Id Cliente</th>\n",
              "      <th>Idade</th>\n",
              "      <th>Preço Seguro</th>\n",
              "      <th>CEP</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>1001</td>\n",
              "      <td>25</td>\n",
              "      <td>801</td>\n",
              "      <td>19001</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>1002</td>\n",
              "      <td>27</td>\n",
              "      <td>1090</td>\n",
              "      <td>19027</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>1003</td>\n",
              "      <td>45</td>\n",
              "      <td>364</td>\n",
              "      <td>19030</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>1004</td>\n",
              "      <td>30</td>\n",
              "      <td>2428</td>\n",
              "      <td>19014</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>1005</td>\n",
              "      <td>32</td>\n",
              "      <td>891</td>\n",
              "      <td>19020</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>\n",
              "      <button class=\"colab-df-convert\" onclick=\"convertToInteractive('df-1a69c10a-56b5-4b7c-884e-bfb2b438b1a0')\"\n",
              "              title=\"Convert this dataframe to an interactive table.\"\n",
              "              style=\"display:none;\">\n",
              "        \n",
              "  <svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\"viewBox=\"0 0 24 24\"\n",
              "       width=\"24px\">\n",
              "    <path d=\"M0 0h24v24H0V0z\" fill=\"none\"/>\n",
              "    <path d=\"M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z\"/><path d=\"M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z\"/>\n",
              "  </svg>\n",
              "      </button>\n",
              "      \n",
              "  <style>\n",
              "    .colab-df-container {\n",
              "      display:flex;\n",
              "      flex-wrap:wrap;\n",
              "      gap: 12px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert {\n",
              "      background-color: #E8F0FE;\n",
              "      border: none;\n",
              "      border-radius: 50%;\n",
              "      cursor: pointer;\n",
              "      display: none;\n",
              "      fill: #1967D2;\n",
              "      height: 32px;\n",
              "      padding: 0 0 0 0;\n",
              "      width: 32px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert:hover {\n",
              "      background-color: #E2EBFA;\n",
              "      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "      fill: #174EA6;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert {\n",
              "      background-color: #3B4455;\n",
              "      fill: #D2E3FC;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert:hover {\n",
              "      background-color: #434B5C;\n",
              "      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);\n",
              "      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));\n",
              "      fill: #FFFFFF;\n",
              "    }\n",
              "  </style>\n",
              "\n",
              "      <script>\n",
              "        const buttonEl =\n",
              "          document.querySelector('#df-1a69c10a-56b5-4b7c-884e-bfb2b438b1a0 button.colab-df-convert');\n",
              "        buttonEl.style.display =\n",
              "          google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "\n",
              "        async function convertToInteractive(key) {\n",
              "          const element = document.querySelector('#df-1a69c10a-56b5-4b7c-884e-bfb2b438b1a0');\n",
              "          const dataTable =\n",
              "            await google.colab.kernel.invokeFunction('convertToInteractive',\n",
              "                                                     [key], {});\n",
              "          if (!dataTable) return;\n",
              "\n",
              "          const docLinkHtml = 'Like what you see? Visit the ' +\n",
              "            '<a target=\"_blank\" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'\n",
              "            + ' to learn more about interactive tables.';\n",
              "          element.innerHTML = '';\n",
              "          dataTable['output_type'] = 'display_data';\n",
              "          await google.colab.output.renderOutput(dataTable, element);\n",
              "          const docLink = document.createElement('div');\n",
              "          docLink.innerHTML = docLinkHtml;\n",
              "          element.appendChild(docLink);\n",
              "        }\n",
              "      </script>\n",
              "    </div>\n",
              "  </div>\n",
              "  "
            ]
          },
          "metadata": {},
          "execution_count": 58
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "Prever = Novas_vendas.iloc[:, 1:4].values\n",
        "Novas_vendas['previsao do modelo'] = floresta1.predict(Prever)\n"
      ],
      "metadata": {
        "id": "6cwTIGpn_xAI"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "Novas_vendas['previsao do modelo'].value_counts()"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "fyhroG9yAnYl",
        "outputId": "c52d4b8e-8737-49f3-9ec9-f87ec298153c"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "1    15\n",
              "2     5\n",
              "3     1\n",
              "Name: previsao do modelo, dtype: int64"
            ]
          },
          "metadata": {},
          "execution_count": 62
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "Novas_vendas.head()"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 206
        },
        "id": "CGP3aJnCAo4H",
        "outputId": "5a96745e-5bc3-45a2-f9ae-8c053621b8d7"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "   Id Cliente  Idade  Preço Seguro    CEP  previsao do modelo\n",
              "0        1001     25           801  19001                   1\n",
              "1        1002     27          1090  19027                   1\n",
              "2        1003     45           364  19030                   1\n",
              "3        1004     30          2428  19014                   1\n",
              "4        1005     32           891  19020                   1"
            ],
            "text/html": [
              "\n",
              "  <div id=\"df-2a6090a7-a98e-4da4-846e-b40038096532\">\n",
              "    <div class=\"colab-df-container\">\n",
              "      <div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>Id Cliente</th>\n",
              "      <th>Idade</th>\n",
              "      <th>Preço Seguro</th>\n",
              "      <th>CEP</th>\n",
              "      <th>previsao do modelo</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>1001</td>\n",
              "      <td>25</td>\n",
              "      <td>801</td>\n",
              "      <td>19001</td>\n",
              "      <td>1</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>1002</td>\n",
              "      <td>27</td>\n",
              "      <td>1090</td>\n",
              "      <td>19027</td>\n",
              "      <td>1</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>1003</td>\n",
              "      <td>45</td>\n",
              "      <td>364</td>\n",
              "      <td>19030</td>\n",
              "      <td>1</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>1004</td>\n",
              "      <td>30</td>\n",
              "      <td>2428</td>\n",
              "      <td>19014</td>\n",
              "      <td>1</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>1005</td>\n",
              "      <td>32</td>\n",
              "      <td>891</td>\n",
              "      <td>19020</td>\n",
              "      <td>1</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>\n",
              "      <button class=\"colab-df-convert\" onclick=\"convertToInteractive('df-2a6090a7-a98e-4da4-846e-b40038096532')\"\n",
              "              title=\"Convert this dataframe to an interactive table.\"\n",
              "              style=\"display:none;\">\n",
              "        \n",
              "  <svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\"viewBox=\"0 0 24 24\"\n",
              "       width=\"24px\">\n",
              "    <path d=\"M0 0h24v24H0V0z\" fill=\"none\"/>\n",
              "    <path d=\"M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z\"/><path d=\"M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z\"/>\n",
              "  </svg>\n",
              "      </button>\n",
              "      \n",
              "  <style>\n",
              "    .colab-df-container {\n",
              "      display:flex;\n",
              "      flex-wrap:wrap;\n",
              "      gap: 12px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert {\n",
              "      background-color: #E8F0FE;\n",
              "      border: none;\n",
              "      border-radius: 50%;\n",
              "      cursor: pointer;\n",
              "      display: none;\n",
              "      fill: #1967D2;\n",
              "      height: 32px;\n",
              "      padding: 0 0 0 0;\n",
              "      width: 32px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert:hover {\n",
              "      background-color: #E2EBFA;\n",
              "      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "      fill: #174EA6;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert {\n",
              "      background-color: #3B4455;\n",
              "      fill: #D2E3FC;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert:hover {\n",
              "      background-color: #434B5C;\n",
              "      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);\n",
              "      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));\n",
              "      fill: #FFFFFF;\n",
              "    }\n",
              "  </style>\n",
              "\n",
              "      <script>\n",
              "        const buttonEl =\n",
              "          document.querySelector('#df-2a6090a7-a98e-4da4-846e-b40038096532 button.colab-df-convert');\n",
              "        buttonEl.style.display =\n",
              "          google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "\n",
              "        async function convertToInteractive(key) {\n",
              "          const element = document.querySelector('#df-2a6090a7-a98e-4da4-846e-b40038096532');\n",
              "          const dataTable =\n",
              "            await google.colab.kernel.invokeFunction('convertToInteractive',\n",
              "                                                     [key], {});\n",
              "          if (!dataTable) return;\n",
              "\n",
              "          const docLinkHtml = 'Like what you see? Visit the ' +\n",
              "            '<a target=\"_blank\" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'\n",
              "            + ' to learn more about interactive tables.';\n",
              "          element.innerHTML = '';\n",
              "          dataTable['output_type'] = 'display_data';\n",
              "          await google.colab.output.renderOutput(dataTable, element);\n",
              "          const docLink = document.createElement('div');\n",
              "          docLink.innerHTML = docLinkHtml;\n",
              "          element.appendChild(docLink);\n",
              "        }\n",
              "      </script>\n",
              "    </div>\n",
              "  </div>\n",
              "  "
            ]
          },
          "metadata": {},
          "execution_count": 64
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        ""
      ],
      "metadata": {
        "id": "Gzndhq60BQm8"
      },
      "execution_count": null,
      "outputs": []
    }
  ]
}
