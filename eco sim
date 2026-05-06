from abc import ABC, abstractmethod
import random

class Organism(ABC):
    def __init__(self, name, energy):
        self.name = name
        self._energy = energy

    def get_energy(self):
        return self._energy

    def decrease_energy(self):
        self._energy -= 1

    def increase_energy(self, val):
        self._energy += val

    @abstractmethod
    def act(self, world):
        pass


class Plant(Organism):
    def act(self, world):
        self.increase_energy(1)
        print(self.name, "is growing. Energy:", self.get_energy())

    def move(self):
        pass


class Animal(Organism):
    @abstractmethod
    def move(self):
        pass


class Herbivore(Animal):
    def move(self):
        print(self.name, "is moving")

    def act(self, world):
        self.move()
        self.decrease_energy()

        for org in world.organisms:
            if isinstance(org, Plant):
                self.increase_energy(3)
                world.organisms.remove(org)
                print(self.name, "ate", org.name, "| Energy:", self.get_energy())
                return

        print(self.name, "found no food | Energy:", self.get_energy())


class Carnivore(Animal):
    def move(self):
        print(self.name, "is hunting")

    def act(self, world):
        self.move()
        self.decrease_energy()

        for org in world.organisms:
            if isinstance(org, Herbivore):
                self.increase_energy(5)
                world.organisms.remove(org)
                print(self.name, "ate", org.name, "| Energy:", self.get_energy())
                return

        print(self.name, "found no prey | Energy:", self.get_energy())


class World:
    def __init__(self):
        self.organisms = []

    def simulate(self, turns):
        for t in range(turns):
            print("\nTurn", t+1)

            for org in self.organisms[:]:
                org.act(self)

            self.organisms = [o for o in self.organisms if o.get_energy() > 0]


# ---- Run ----

world = World()

world.organisms.append(Plant("Grass", 5))
world.organisms.append(Plant("Bush", 5))

world.organisms.append(Herbivore("Deer", 10))
world.organisms.append(Herbivore("Rabbit", 10))

world.organisms.append(Carnivore("Lion", 15))
world.organisms.append(Carnivore("Bear", 15))

world.simulate(5)
