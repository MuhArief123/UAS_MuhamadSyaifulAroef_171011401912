{
  "nbformat": 4,
  "nbformat_minor": 0,
  "metadata": {
    "colab": {
      "name": "UAS_Muhamad Syaiful Arief_171011401912.ipynb",
      "provenance": [],
      "authorship_tag": "ABX9TyMUXxZ/gjooRQ6w9ZRcupMj",
      "include_colab_link": true
    },
    "kernelspec": {
      "name": "python3",
      "display_name": "Python 3"
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
        "<a href=\"https://colab.research.google.com/github/MuhArief123
/
/UAS_MuhamadSyaifulArief_171011401912.ipynb/blob/main/UAS_MuhamadSyaifulArief_171011401912.ipynb\" target=\"_parent\"><img src=\"https://colab.research.google.com/assets/colab-badge.svg\" alt=\"Open In Colab\"/></a>"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "T4yZqdyq0SKK"
      },
      "source": [
        " import pandas as pd\n",
        "import pydotplus #pip install pydotplus\n",
        "from sklearn.tree import export_graphviz\n",
        "from sklearn.tree import DecisionTreeClassifier\n",
        "import numpy as np\n",
        "from matplotlib import pyplot as plt"
      ],
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "GzcTcjdOYyxM"
      },
      "source": [
        "Buat Data Tiruan untuk mengklasifikasikan jenis kelamin berdasarkan berat badan. Untuk laki-laki ditandai dengan angka 1 dan wanita angka 0."
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 359
        },
        "id": "BGoDiy9E0tEa",
        "outputId": "a64b4291-d08e-48d1-9d5b-28cb9c9399c1"
      },
      "source": [
        " data = pd.DataFrame({'Berat Badan': [42,45,52,75,62,65,70,50,55,80], \n",
        "             'Jenis Kelamin': [1,0,1,0,1,0,0,1,1,0]})\n",
        "data =data.sort_values('Berat Badan')\n",
        "data"
      ],
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/html": [
              "<div>\n",
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
              "      <th>Berat Badan</th>\n",
              "      <th>Jenis Kelamin</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>42</td>\n",
              "      <td>1</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>45</td>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>7</th>\n",
              "      <td>50</td>\n",
              "      <td>1</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>52</td>\n",
              "      <td>1</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>8</th>\n",
              "      <td>55</td>\n",
              "      <td>1</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>62</td>\n",
              "      <td>1</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>5</th>\n",
              "      <td>65</td>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>6</th>\n",
              "      <td>70</td>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>75</td>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>9</th>\n",
              "      <td>80</td>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>"
            ],
            "text/plain": [
              "   Berat Badan  Jenis Kelamin\n",
              "0           42              1\n",
              "1           45              0\n",
              "7           50              1\n",
              "2           52              1\n",
              "8           55              1\n",
              "4           62              1\n",
              "5           65              0\n",
              "6           70              0\n",
              "3           75              0\n",
              "9           80              0"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 15
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 234
        },
        "id": "ex4uVRg7MQ_v",
        "outputId": "b220fe6e-09de-4d8c-817a-40cc744eed38"
      },
      "source": [
        "plt.plot([42,45,52,75,62,65,70,50,55,80],[1,0,1,0,1,0,0,1,1,0])"
      ],
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "[<matplotlib.lines.Line2D at 0x7f9a121503c8>]"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 14
        },
        {
          "output_type": "display_data",
          "data": {
            "image/png": "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\n",
            "text/plain": [
              "<Figure size 432x288 with 1 Axes>"
            ]
          },
          "metadata": {
            "tags": [],
            "needs_background": "light"
          }
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "oPThcZaPOdv5"
      },
      "source": [
        " def tree_graph_to_png(tree, feature_names, png_file_to_save):\n",
        "    tree_str = export_graphviz(tree, feature_names=feature_names, \n",
        "                                     filled=True, out_file=None)\n",
        "    graph = pydotplus.graph_from_dot_data(tree_str)  \n",
        "    graph.write_png(png_file_to_save)"
      ],
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "r4Hr9-0cO5Nr"
      },
      "source": [
        " #define Decision Tree\n",
        "dt = DecisionTreeClassifier(criterion = 'entropy')\n",
        "#Define input vectors\n",
        "#X is the features in this dataset\n",
        "X = data['Berat Badan'].values.reshape(-1, 1)\n",
        "#Y is the vector with our Target Variables\n",
        "Y = data['Jenis Kelamin'].values\n",
        "#start fitting process\n",
        "dt.fit(X, Y)\n",
        " \n",
        "tree_graph_to_png(dt, feature_names=['Berat Badan'], \n",
        "                 png_file_to_save='dt.png')"
      ],
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "rh-iumSpPWFB",
        "outputId": "c4accc21-d77a-40dd-e480-169400af21b4"
      },
      "source": [
        " d  = np.array([7, 15, 43, 45])\n",
        "d=d.reshape(-1, 1)\n",
        " \n",
        "dt.predict(d)"
      ],
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "array([1, 1, 1, 0])"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 24
        }
      ]
    }
  ]
} 
