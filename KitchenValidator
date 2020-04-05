package org.xtext.example.mydsl

import org.eclipse.xtext.validation.Check
import org.dsl.ruuhijärvi.CookingLanguage

class KitchenValidator {
	
	@Check
	def checkNoCycleInHierarchy(Entity entity) {
		if (entity.superType == null)
			return
			
		val visitedEntities = newHashSet(entity)
		
		var current = entity.superType
		while (current != null) {
			if (visitedEntities.contains(current)) {
				error("Cycle in hierarchy of entity '" + current.name + "'", 
					EntitiesPackage.eINSTANCE.entity_SuperType)
				return
			}
			visitedEntities.add(current)
			current = current.superType
		}
	}
	
	@Check
	def checkFieldNameIsInRecipeDatabase(Field field) {
		if (field.type instanceof Basictype
			&&
			(field.type as BasicType).typeName == 'recipe'
			&&
			! field.name.charAt(0).noMatchFound)
				warning("Field name is not a known recipe name. Check for spelling mistakes", 
					EntitiesPackage.eINSTANCE.field_Name
			)
	}
	
	@Check
	def checkFieldIsCorrectUnitType(Field field) {
		if (field.type instanceof BasicType
			&&
			(field.type as BasicType).typeName == 'unit'
			&&
			! field.name.charAt(0).NotaUnit)
				warning("Unit type not supported. Use only supported unit types", 
					EntitiesPackage.eINSTANCE.unit_name
			)
	}
}
