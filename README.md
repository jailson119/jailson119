import datetime

class GymManagementSystem:
    def __init__(self):
        self.members = []
        self.classes = []
        self.equipment_inventory = []
        self.activity_log = []

    # Gestão de Membros
    def add_member(self, name, subscription_plan):
        member_id = len(self.members) + 1  # Atribuir ID automático incremental
        member = {'member_id': member_id, 'name': name, 'subscription_plan': subscription_plan, 'join_date': datetime.date.today()}
        self.members.append(member)
        self.activity_log.append(f"Novo membro adicionado: {name}")

    def remove_member(self, member_id):
        for member in self.members:
            if member['member_id'] == member_id:
                self.members.remove(member)
                self.activity_log.append(f"Membro removido: {member['name']}")
                break
        else:
            print("Membro não encontrado")

    def view_member_details(self, member_id):
        for member in self.members:
            if member['member_id'] == member_id:
                print(f"Detalhes do Membro:\nNome: {member['name']}\nID: {member['member_id']}\nPlano: {member['subscription_plan']}")
                return
        print("Membro não encontrado")

    # Agendamento de Aulas
    def schedule_class(self, class_name, instructor, room, date, time):
        gym_class = {'class_name': class_name, 'instructor': instructor, 'room': room, 'date': date, 'time': time}
        self.classes.append(gym_class)
        self.activity_log.append(f"Aula agendada: {class_name}")

    def cancel_class(self, class_name):
        for gym_class in self.classes:
            if gym_class['class_name'] == class_name:
                self.classes.remove(gym_class)
                self.activity_log.append(f"Aula cancelada: {class_name}")
                break
        else:
            print("Aula não encontrada")

    def view_class_schedule(self):
        print("Horário das Aulas:")
        for gym_class in self.classes:
            print(f"{gym_class['class_name']} - {gym_class['instrutor']} - {gym_class['room']} - {gym_class['date']} {gym_class['time']}")

    # Inventário de Equipamentos
    def add_equipment(self, equipment_name):
        equipment = {'equipment_name': equipment_name, 'last_used': None}
        self.equipment_inventory.append(equipment)
        self.activity_log.append(f"Novo equipamento adicionado: {equipment_name}")

    def remove_equipment(self, equipment_name):
        for equipment in self.equipment_inventory:
            if equipment['equipment_name'] == equipment_name:
                self.equipment_inventory.remove(equipment)
                self.activity_log.append(f"Equipamento removido: {equipment_name}")
                break
        else:
            print("Equipamento não encontrado")

    def perform_maintenance(self, equipment_name):
        for equipment in self.equipment_inventory:
            if equipment['equipment_name'] == equipment_name:
                equipment['last_used'] = None
                self.activity_log.append(f"Manutenção realizada em: {equipment_name}")
                break
        else:
            print("Equipamento não encontrado")

    def rent_equipment(self, member_id, equipment_name):
        for member in self.members:
            if member['member_id'] == member_id:
                for equipment in self.equipment_inventory:
                    if equipment['equipment_name'] == equipment_name:
                        if equipment['last_used'] is not None:
                            print(f"Equipamento '{equipment_name}' já está alugado")
                            return
                        equipment['last_used'] = datetime.datetime.now()
                        print(f"{member['name']} alugou {equipment_name}")
                        return
                print(f"Equipamento '{equipment_name}' não encontrado")
                return
        print(f"Membro com ID '{member_id}' não encontrado")

    def generate_report(self):
        # Adicione lógica para gerar relatórios
        report = "Relatório: ...\n"  # Substitua isso pela lógica real de geração de relatórios
        print(report)
        self.activity_log.append("Relatório gerado")

    def log_activity(self, activity_description):
        self.activity_log.append(activity_description)

    # Interface de Utilizador
    def _display_menu(self):
        print("1. Adicionar Membro")
        print("2. Remover Membro")
        print("3. Visualizar Detalhes do Membro")
        print("4. Agendar Aula")
        print("5. Cancelar Aula")
        print("6. Visualizar Horário das Aulas")
        print("7. Adicionar Equipamento")
        print("8. Remover Equipamento")
        print("9. Realizar Manutenção em Equipamento")
        print("10. Alugar Equipamento")
        print("11. Gerar Relatório")
        print("12. Registrar Atividade")
        print("13. Sair")

    def run_system(self):
        print("Bem-vindo ao Sistema de Gestão de Academia!")
        while True:
            self._display_menu()
            choice = input("Escolha uma opção: ")

            if choice == '1':
                name = input("Digite o nome do membro: ")
                subscription_plan = input("Digite o plano de assinatura: ")
                self.add_member(name, subscription_plan)
            elif choice == '2':
                member_id = int(input("Digite o ID do membro a ser removido: "))
                self.remove_member(member_id)
            elif choice == '3':
                member_id = int(input("Digite o ID do membro: "))
                self.view_member_details(member_id)
            elif choice == '4':
                class_name = input("Digite o nome da aula: ")
                instructor = input("Digite o nome do instrutor: ")
                room = input("Digite o nome da sala: ")
                date = input("Digite a data da aula (DD/MM/AAAA): ")
                time = input("Digite o horário da aula: ")
                self.schedule_class(class_name, instructor, room, date, time)
            elif choice == '5':
                class_name = input("Digite o nome da aula a ser cancelada: ")
                self.cancel_class(class_name)
            elif choice == '6':
                self.view_class_schedule()
            elif choice == '7':
                equipment_name = input("Digite o nome do equipamento: ")
                self.add_equipment(equipment_name)
            elif choice == '8':
                equipment_name = input("Digite o nome do equipamento a ser removido: ")
                self.remove_equipment(equipment_name)
            elif choice == '9':
                equipment_name = input("Digite o nome do equipamento a receber manutenção: ")
                self.perform_maintenance(equipment_name)
            elif choice == '10':
                member_id = int(input("Digite o ID do membro: "))
                equipment_name = input("Digite o nome do equipe")


if __name__ == "__main__":
    gym_system = GymManagementSystem()
    gym_system.run_system() 

