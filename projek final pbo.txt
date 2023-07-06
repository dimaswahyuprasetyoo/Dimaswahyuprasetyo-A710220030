from PyQt5.QtWidgets import QApplication, QMainWindow, QLabel, QPushButton, QLineEdit, QGridLayout, QWidget
from PyQt5.QtGui import QIcon

class IMTCalculator(QMainWindow):
    def __init__(self):
        super().__init__()
        self.setWindowTitle('Kalkulator IMT')
        self.setWindowIcon(QIcon('path_to_your_image.png')) 
        self.initUI()

    def initUI(self):

        if __name__ == '__main__':
            app = QApplication([])
            window = IMTCalculator()
            window.show()
            app.exec_()


    def initUI(self):
        self.age_label = QLabel("Umur:")
        self.age_input = QLineEdit()
        self.height_label = QLabel("Tinggi (cm):")
        self.height_input = QLineEdit()
        self.weight_label = QLabel("Berat (kg):")
        self.weight_input = QLineEdit()
        self.gender_label = QLabel("Jenis Kelamin:")
        self.gender_male_button = QPushButton('Laki-laki')
        self.gender_male_button.clicked.connect(self.calculate_imt)
        self.gender_female_button = QPushButton('Perempuan')
        self.gender_female_button.clicked.connect(self.calculate_imt)
        self.result_label = QLabel()

        layout = QGridLayout()
        layout.addWidget(self.age_label, 0, 0)
        layout.addWidget(self.age_input, 0, 1)
        layout.addWidget(self.height_label, 1, 0)
        layout.addWidget(self.height_input, 1, 1)
        layout.addWidget(self.weight_label, 2, 0)
        layout.addWidget(self.weight_input, 2, 1)
        layout.addWidget(self.gender_label, 3, 0)
        layout.addWidget(self.gender_male_button, 3, 1)
        layout.addWidget(self.gender_female_button, 3, 2)
        layout.addWidget(self.result_label, 4, 0, 1, 3)

        container = QWidget()
        container.setLayout(layout)
        self.setCentralWidget(container)

        # Set background color
        container.setStyleSheet("background-color: silver;")
        self.result_label.setStyleSheet("background-color: white; padding: 10px;")

    def calculate_imt(self):
        age = int(self.age_input.text())
        height = float(self.height_input.text())
        weight = float(self.weight_input.text())

        gender = ""
        if self.sender() == self.gender_male_button:
            gender = "Laki-laki"
        elif self.sender() == self.gender_female_button:
            gender = "Perempuan"

        imt = weight / ((height/100) ** 2)
        category = ""

        if imt < 18.5:
            category = "Kurus"
        elif imt >= 18.5 and imt < 25:
            category = "Normal"
        elif imt >= 25 and imt < 30:
            category = "Kelebihan Berat Badan"
        else:
            category = "Obesitas"

        result = f"<b>Umur:</b> {age}<br><b>Tinggi:</b> {height} cm<br><b>Berat:</b> {weight} kg<br><b>Jenis Kelamin:</b> {gender}<br><b>IMT:</b> {imt:.2f}<br><b>Kategori:</b> {category}"

        self.result_label.setText(result)

if __name__ == '__main__':
    app = QApplication([])
    window = IMTCalculator()
    window.show()
    app.exec_()
