Whiteboarding

class Array
  
  def merge_sort(&prc)
    prc ||= Proc.new { |num1, num2| num1 <=> num2 } 
    return self if self.count <= 1
    middle = self.length / 2
    left = self[0...middle]
    right = self[middle..-1]
    
    left_sorted = left.merge_sort(&prc)
    right_sorted = right.merge_sort(&prc)

    self.merge(left_sorted, right_sorted, &prc)

  end 

  def self.merge(left, right, &prc)
    sorted_numbers = []
    until left.empty? || right.empty? 
        case prc.call(left[0], right[0]) 
        when -1 
        sorted_numbers << left.shift
        when 0 
            sorted_numbers << left.shift
        when 1
            sorted_numbers << right.shift
        end
    end
    sorted_numbers + left + right
  end
  
end

#monkey patch into array class
#create a my each method
#takes in block



class Array 
  def my_each(&prc)
    i = 0
    while i < self.length
      prc.call(self[i])
      i += 1
    end
    self
  end
end

# hash - keys are duplicate eles, values are indices for eles 

class Array 
  def dups
    indices = Hash.new { |indices, el| indices[el] = [] }
    self.each_with_index do |el, idx|
      indices[el] << idx
    end
    indices.select { |indices, el| el.length > 1 }
  end
end

arr = [1, 1, 0, 5, 1, 1]

# finds first n factorial nums 
# 0! => 1, 1! => 1, 2! => 2

def rec_factorials(num)
  return [1] if num == 1
  factorials = rec_factorials(num - 1)
  factorials << factorials.last * (num - 1)
  factorials
end


def factorials_rec(num)
  return [] if num == 0
  return [1] if num == 1
  return [1, 1] if num == 2

  arr = [factorial(num-1)]
  arr = factorials_rec(num-1) + arr
  

end

def factorial(num)
  return 1 if num == 0
  mult = 1
  (1..num).each do |ele|
    mult = mult * ele
  end
  mult
end


def factorials_rec(num)
  if num == 1
    [1]
  else
    facs = factorials_rec(num - 1)
    facs << facs.last * (num - 1)
    facs
  end
end


def factorials_rec(num)
  if num == 1
    [1]
  else
    facs = factorials_rec(num - 1)
    facs << facs.last * (num - 1)
    facs
  end
end